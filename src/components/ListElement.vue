<template>
<section>
  
    <CoinDetails 
        v-if="clicked"
        :coin="clickList()" 
    /> <!-- CoinDetails should be rendered on click with the method clickList and pass the coin object/element to CoinDetails -->
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
            <tr v-for="(row, index) in coin" :key="index" @click="clickList(row, index)">
                <td>
                {{ row.market_cap_rank }}
                </td>
                <td>
                    <img :src="row.image" width="15" height="15">
                    <span class="coin-name">&emsp;{{ row.id }}&ensp;</span>
                    <span class="symbol">{{ row.symbol.toUpperCase() }}</span>
                </td>
                <td>
                    <span class="symbol"> {{ row.current_price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") }} € </span>
                </td>        
                <td>
                    <span v-if="row.price_change_percentage_24h >= 0" class="desc green">{{ row.price_change_percentage_24h }} %</span>
                    <span v-else class="desc red">{{ row.price_change_percentage_24h }} %</span>
                </td> 
                <td>
                    <span class="desc">{{ row.total_volume.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") }} €</span>
                </td>
            </tr> 
        </tbody>  
    </table>
</section>
</template>

<script>
import CoinDetails from "./CoinDetails.vue"

export default {
    props: [ 'coin' ],
    components: {
    CoinDetails
},
    data() {
        return {
            clicked: false,
            isGreen: true
        }
    },

    computed: {
        computedClass() {
            if ( this.coin.price_change_percentage_24h >= 0) {
                return 'green'
            }
            return 'red'
        },
    },

    methods: {
        clickList: function (row, index) {
            console.log("clicked ", row, index) // TO FIX: row and index are undefined
            this.clicked = !this.clicked
            return {
                row: this.row,
                index: this.index
            }
        }
    }

}
</script>

<style>
hr {
    border-top: 0.6px solid #cccccc;
}
.table {
    margin-top: 0.5rem;
}
.coin-name {
    font-weight: 600;
    font-size: 0.95rem;
    color: #0862CC;
}
.coin-name:hover {
    text-decoration: underline;
    letter-spacing: 0.005rem;
}
.coin-header:hover .icon {
    fill:rgb(245, 245, 21);
    stroke:rgb(223, 223, 40);
}
.coin-header:hover .symbol {
    color:rgb(223, 223, 40);
}
.icon {
    fill: none;
    vertical-align: middle;
    stroke: #666666;
}
.symbol {
    vertical-align: middle;
    font-size: 0.8rem;
    font-weight: 500;
    color: #595959;
}
.desc {
    font-size: 0.8rem;
}
.green {
    color: rgb(0, 207, 0);
}
.red {
    color: red;
}
</style>