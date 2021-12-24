<template>
  <div id="app">
    <Header />
    <div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <HelloWorld />
    <Body></Body>
    </div>
    <div>
      <Footer />
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Header from "./components/Header.vue";
import Body from "./components/Body.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Header,
    Body,
    Footer,
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
  /* margin-top: 60px; */
}
</style>
