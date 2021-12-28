<template>
  <div id="app">
    <div id="body">
      <Header @clicked_search="getClickedSearchItem" />
      <div>
        <Body :searched_data="searched_data" :show_search="show_search" />
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    Header,
    Body,
    Footer,
  },
  data() {
    return {
      searched_data: "",
      show_search: false,
    };
  },
  methods: {
    getClickedSearchItem(data, isShow) {
      this.searched_data = data;
      this.show_search = isShow;
    },
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
  background-image: url("https://olvy.s3.amazonaws.com/hero-background.svg");
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
}
</style>
