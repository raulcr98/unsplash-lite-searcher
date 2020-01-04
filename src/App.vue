<template>
  <div id="app">
    <Header />
    <Searcher />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Searcher from "./components/Searcher.vue";

export default {
  name: "app",
  components: {
    Header,
    Searcher,
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 2px;
}
</style>
