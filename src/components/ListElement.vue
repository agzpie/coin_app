<template>
    <div>
        <hr>
        <p class="coin-header">
            <span class="coin-name"> coind id </span>
            &ensp;
            <svg class="icon" width="15" height="13" viewBox="0 0 15 14" xmlns="http://www.w3.org/2000/svg">
                <path class="icon" d="M7.5 1L9.33389 4.97587L13.6819 5.49139L10.4673 8.46413L11.3206 12.7586L7.5 10.62L3.6794 12.7586L4.5327 8.46413L1.31813 5.49139L5.66611 4.97587L7.5 1Z" stroke-width="1.2" stroke-linejoin="round"/>
            </svg>

            <span class="symbol"> coin symbol</span>
        </p>
        <p class="desc"> coin current_price </p>
    </div>
</template>

<script>
export default {
    //props: [ 'coin' ],
}
</script>

<style>
hr {
    border-top: 0.6px solid #cccccc;
}
.coin-name {
    font-weight: 600;
    font-size: 1rem;
    color: #0862CC;
    /* TODO make repository name a link */
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
</style>