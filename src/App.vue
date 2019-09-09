<template>
  <div id="app">
    <navbar />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
export default {
  name: "app",
  components: { Navbar }
};
</script>

<style>
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
