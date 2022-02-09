<template>
  <div class="container-md">
    <Suspense>
      <List />
    </Suspense>
      

  </div>
</template>

<script>
import List from "./components/List";

export default {
  name: "App",
  components: {
    List,
  }
}
</script>

<style>
body {
  background-color: whitesmoke;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}/*
.main {
  width: fit-content;
  margin: auto;
  background-color: white;
  padding: 0.6rem 1.5rem;
  border: 1px solid #2c3e50;
  border-radius: 10px;
  transition: 3s;
  transition-timing-function: ease;
  align-content: space-around;
}*/

</style>