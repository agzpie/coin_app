<template>
<div>
  <h2 class="header1">Which Coin would you like to see?</h2>

    <div class="row g-3 align-items-center">
        <div class="col-auto">
            <input type="text" id="inputCoin" class="form-control" placeholder="Search Coin"
                name="coin-name"
                required 
            />
        </div>
        <div class="col-auto">
            <span id="passwordHelpInline" class="form-text">
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
    <Pagination 
        :totalRecords="coins.length" 
        :perPageOptions="perPageOptions"
        v-model="pagination"    
    />
    {{ pagination.page }}
    <table class="table table-hover">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">Coin</th>
                <th scope="col">Price</th>
                <th scope="col">Price Change</th>
                <th scope="col">24 Volume</th>
            </tr>
        </thead>
        <tbody>
            <ListElement 
                v-for="item in coins"
                :key="item.id"
                :coin="item"
                :priceChange="item.price_change_percentage_24h"
            />
        </tbody>
    </table>
    
    
</div>
</template>

<script>
import ListElement from "./ListElement.vue";
import Pagination from "./Pagination.vue";
import axios from "axios";

const perPageOptions = [10, 25, 50]

export default {
  name: "App",
  components: {
    ListElement,
    Pagination
},
  data: function () {
        return {
            perPageOptions,
            pagination: { page: 1, perPage: perPageOptions[0] },
            coins: [],
            errors: [],

    }
  },

  // Fetches posts when the component is created.
  async created() {
    try {
      const response = await axios.get(`https://api.coingecko.com/api/v3/coins/markets?vs_currency=eur&order=market_cap_desc&per_page=100&page=1&sparkline=false`)
      this.coins = response.data
      console.log(this.coins)
    } catch (e) {
      this.errors.push(e)
    }
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