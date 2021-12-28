<template>
  <div id="app">
    <!-- Main Body include Header component and Body component   -->
    <div id="main_body">
      <!-- HEADER Component :getClickedSearchItem() function invoke when user click on search button or press Enter on Input field  -->
      <Header @clicked_search="getClickedSearchItem" />
      <div>
        <!-- BODY component is pass with searched_data and show_search varibales to display the result -->
        <Body :searched_data="searched_data" :show_search="show_search" />
      </div>
    </div>
    <!-- Footer is outside the main body and at bottom -->
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
      // Variables to store the result from header component and sent back to Body component
      searched_data: "",
      show_search: false,
    };
  },
  methods: {
    // getClickedSearchItem() function : store the values, which is comming from Header Component
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
