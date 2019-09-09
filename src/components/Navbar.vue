<template>
  <nav>
    <component v-if="brandIsFunction" :is="config.brand()" />
    <header v-else>
      <h3>{{ config.brand }}</h3>
    </header>

    <ul
      v-if="canRenderLinks && !renderRouterLinks && !renderCustomLinks"
      :class="renderCustomClass(config.ulClass, 'nav-links')"
    >
      <li v-for="link in config.links" :key="link.to" :class="renderCustomClass(config.liClass)">
        <a :href="link.to" :class="renderCustomClass(config.aClass)" v-if="link.icon">
          <component :is="link.icon()" />
          {{ link.value }}
        </a>
        <a :href="link.to" :class="renderCustomClass(config.aClass)" v-else>{{ link.value }}</a>
      </li>
    </ul>
    <ul
      v-else-if="canRenderLinks && renderRouterLinks"
      :class="renderCustomClass(config.ulClass, 'nav-links')"
    >
      <li v-for="link in config.links" :key="link.to" :class="renderCustomClass(config.liClass)">
        <router-link :to="link.to" :class="renderCustomClass(config.liClass)" v-if="link.icon">
          <component :is="link.icon()" />
          {{ link.value }}
        </router-link>
        <router-link
          :to="link.to"
          :class="renderCustomClass(config.liClass)"
          v-else
        >{{ link.value }}</router-link>
      </li>
    </ul>
    <component
      v-else-if="canRenderLinks && renderCustomLinks"
      :is="config.customLinksComponent()"
      :links="config.links"
    />
  </nav>
</template>

<script>
export default {
  name: "navbar",
  props: {
    config: {
      type: Object
    }
  },
  methods: {
    renderCustomClass(customClass, defaultClass = undefined) {
      return customClass ? customClass : defaultClass;
    }
  },
  computed: {
    renderCustomLinks() {
      return typeof this.config.customLinksComponent === "function";
    },
    renderRouterLinks() {
      return this.config.useAnchor === false;
    },
    canRenderLinks() {
      return typeof this.config.links === "object";
    },
    useAnchorIsBoolean() {
      return typeof this.config.useAnchor === "boolean";
    },
    brandIsFunction() {
      return typeof this.config.brand == "function";
    }
  }
};
</script>

<style scoped src="@/assets/style.css"></style>
