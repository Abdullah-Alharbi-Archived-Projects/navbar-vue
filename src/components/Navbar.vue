<template>
  <nav>
    <div class="menu-icon">
      <div class="line"></div>
      <div class="line"></div>
      <div class="line"></div>
    </div>

    <ul>
      <li>
        <a href="#">Link</a>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "navbar",
  props: {
    config: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
</style>