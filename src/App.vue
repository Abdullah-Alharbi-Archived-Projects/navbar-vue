<template>
  <div id="app">
    <navbar :config="navbar" @menu-click="handleMobileMode" />

    <h1>Custom navbar component</h1>
  </div>
</template>

<script>
import Navbar from "./components/Navbar";

export default {
  name: "app",
  components: { Navbar },
  data() {
    return {
      navbar: {
        brand: "my-awesome-navbar",
        links: [
          {
            to: "?",
            value: "Home"
          },
          {
            to: "?",
            value: "About"
          },
          {
            to: "?",
            value: "Projects"
          }
        ],
        mobileMode: false
      }
    };
  },
  methods: {
    handleMobileMode() {
      this.navbar.mobileMode = !this.navbar.mobileMode;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
