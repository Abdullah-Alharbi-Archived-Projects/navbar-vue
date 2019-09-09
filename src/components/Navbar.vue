<template>
  <nav>
    <!-- dynamic component goes here -->
    <component v-if="typeof config.brand == 'function'" :is="config.brand()" />
    <header v-else>
      <!-- set string in h3 -->
      <h3>{{ config.brand }}</h3>
    </header>
  </nav>
</template>

<script>
export default {
  name: "navbar",
  props: {
    config: {
      type: Object
    }
  }
};
</script>

<style scoped>
</style>