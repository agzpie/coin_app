<template>
  <div class="container-md">
    <Suspense>
      <template #default>
        <List />
      </template>
      <template #fallback>
        <div>Loading...</div>
      </template>
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
}
</style>