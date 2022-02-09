<template>
<tr>
    <td>
    {{ coin.market_cap_rank }}
    </td>
    <td>
        <img :src="coin.image" width="15" height="15">
        <span class="coin-name">&emsp;{{ coin.id }}&ensp;</span>
        <span class="symbol">{{ toCapitals }}</span>
    </td>
    <td>
        <span class="symbol"> {{ coin.current_price }} € </span>
    </td>        
    <td>
        <span class="desc" :class='computedClass'>{{ coin.price_change_percentage_24h }} %</span>
    </td> 
    <td>
        <span class="desc">{{ coin.total_volume }} €</span>
    </td>
</tr>
           
    
</template>

<script>
export default {
    props: {
        coin: Object,
        priceChange: Number,
    }, 

    computed: {
        computedClass() {
            if ( this.priceChange >= 0) {
                return 'green'
            }
            return 'red'
        },

        toCapitals() {
            return this.coin.symbol.toUpperCase()
        }
    },

}
</script>

<style>
hr {
    border-top: 0.6px solid #cccccc;
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