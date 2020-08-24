<template>
  <div id="app">
    <TopBar />
    <div class="contents">
      <BooksSearch />
    </div>
  </div>
</template>

<script>
import BooksSearch from "./components/Search.vue";
import TopBar from "./components/Top.vue";

export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    BooksSearch,
    TopBar,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.contents {
  width: 100%;
  padding-top: 6em;
}
</style>
