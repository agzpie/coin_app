<template>
<div>
  <h2 class="header1">Which Coin would you like to see?</h2>

    <div class="container">
      <div class="form-container">
        <input
          v-model="name"
          id="coin-name"
          name="coin-name"
          placeholder="Search Coin"
          required
        />
      </div>
      <div class="btn-container">
        <button
          class="accept-button"
          @click="
            coinName = name;
            isActive = false;
          "
        >
          OK
        </button>
      </div>
    </div>

    <h4 v-if="success == true">
      The most popular coinzz:
    </h4>
    <h4 v-else-if="success == false" class="error-message">
      Oopsie,<br />there was an error,<br />
      but don't worry and try again!
    </h4>

    <table>
        <tr>
            <th>#</th>
            <th>Coin</th>
            <th>Price</th>
            <th>Price Change</th>
            <th>24 Volume</th>
        </tr>
        <ListElement 
    v-for="item in coins"
    :key="item.id"
    :coin="item"
    />
    </table>
    
    
</div>
</template>

<script>
import ListElement from "./ListElement.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    ListElement,
  },
  data() {
    return {
      coins: [],
      errors: []
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
.container {
  display: flex;
  padding-top: 0.4rem;
  padding-bottom: 0.8rem;
}
.form-container {
  align-self: flex-start;
  flex-grow: 1;
}
.btn-container {
  justify-content: center;
  flex-grow: 1;
}
.accept-button {
  align-self: center;
  color: white;
  font-weight: 600;
  background: rgb(34, 158, 94);
  background: radial-gradient(circle, #31a851 28%, rgba(31, 149, 52, 1) 78%);
  background-size: 100% auto;
  padding: 0.25rem 1.5rem;
  position: center;
  border: 1px solid #2c3e50;
  border-radius: 5px;
  transition: 0.3s all ease;
  cursor: pointer;
  box-shadow: 0 2px 10px rgb(217, 236, 220);
  /* TODO button background is too high on hover */
}
.accept-button:hover {
  background-size: 170%;
  background-position: center;
  box-shadow: 0 6px 16px rgb(202, 226, 205);
  transform: translate(0px, -1px);
  letter-spacing: 0.05rem;
}
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