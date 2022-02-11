<template>
<div>
  <h2 class="header1">Which Coin would you like to see?</h2>

    <div class="row g-3 align-items-center">
        <div class="col-auto">
           <input type="text" id="search" class="form-control" placeholder="Search Coin" v-model="term" @keypress.enter="search(term)" />
        </div>
        <div class="col-auto">
            <span class="form-text">
                Search by coin's name or symbol.
            </span>
        </div>
    </div>

    <!--<h4 v-if="success == true">
      The most popular coinzz:
    </h4>
    <h4 v-else-if="success == false" class="error-message">
      Oopsie,<br />there was an error,<br />
      but don't worry and try again!
    </h4>-->

    <ListElement 
        v-if="coins"
        :coin="computedCoinList"
    /> 
    <div class="pagination">

    <Pagination 
        v-if="coins"
        :totalRecords="coins.length" 
        :perPageOptions="perPageOptions"
        v-model="pagination" 
        ref="searchField"   
    />
    </div>
</div>
</template>

<script>
// TODO: reset coin list!!!! And detailed view
import ListElement from "./ListElement.vue";
import Pagination from "./Pagination.vue";
import axios from "axios";

const perPageOptions = [10, 25, 50]

export default {
    name: "App",
    components: {
        ListElement,
        Pagination,
    },
    data: function () {
        return {
            perPageOptions,
            coins: undefined,
            pagination: { page: 1, perPage: perPageOptions[0] },
        }
    },
    computed: {
        computedCoinList () {
            console.log("cos")
            if (!this.coins) {
                console.log("ERROR: Data is empty")
                return []
            }
            else {
                const firstIndex = (this.pagination.page - 1) * this.pagination.perPage
                const lastIndex = this.pagination.page * this.pagination.perPage
                return this.coins.slice(firstIndex, lastIndex)
            }
        }
    },

    // Fetch coin data
    mounted () {
        axios
            .get('https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false')
            .then(response => {
                this.coins = response.data
                console.log(this.coins)
                })
            .catch(error => console.log(error))
    },

   /* async mounted() {
        try {
        const response = await axios.get(`https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false`)
        this.coins = response.data
        console.log(this.coins)
        console.log(this.coins.lastIndex)
        } catch (e) {
        this.errors.push(e)
        }
    }*/

    methods: {
        search (term) { // TODO: reset list when search field gets empties
            this.coins = this.coins.filter((coin) => {
            this.$refs.searchField.changePage(0)
                return coin.id.includes(term) || coin.symbol.includes(term)
            })
        },
    }
};
</script>

<style>
.error-message {
  color: rgb(255, 0, 0);
  text-decoration: underline;
  transition: 2s;
}
/* Extra small devices (phones, 450px and down) */
@media only screen and (max-width: 450px) {
  .container {
    flex-wrap: wrap;
    flex-direction: column;
    justify-content: space-evenly;
    height: 20vw;
    align-items: center;
  }
}
</style>