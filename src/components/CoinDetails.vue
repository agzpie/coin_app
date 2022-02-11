<template>
<table class="table table-hover">
   
        <tr>
            <th scope="col">Name</th>
            <td>{{ coin.id }}</td>
        </tr>
        <tr>
            <th scope="col">Symbol</th>
            <td>{{ coin.symbol }}</td>
        </tr>
        <tr>
            <th scope="col">Logo</th>
            <td>{{ coin.image }}</td>
        </tr>
        
</table>
</template>

<script>
export default {
    props: {
        coin: { // TO FIX: data isn't passed properly from the parent
            row: [],
            index: []
        }
    },

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