<template>
  <nav :class="renderCustomClass(config.ulClass, 'navbar')">
    <div class="hamburger" @click="handleMenuClick">
      <div class="line"></div>
      <div class="line"></div>
      <div class="line"></div>
    </div>
    <div class="children">
      <component v-if="brandIsFunction" :is="config.brand()" />
      <div class="position" v-else>
        <header class="header-w">
          <a
            href="/"
            :class="renderCustomClass(config.brandClass, 'brand-link')"
            v-if="!renderRouterLinks && !renderCustomLinks"
          >
            <h3>{{ config.brand }}</h3>
          </a>
          <router-link
            to="/"
            :class="renderCustomClass(config.brandClass, 'brand-link')"
            v-else-if="renderRouterLinks"
          >
            <h3>{{ config.brand }}</h3>
          </router-link>
        </header>
      </div>

      <div class="hamburger" @click="handleMenuClick" v-if="false">
        <div class="line"></div>
        <div class="line"></div>
        <div class="line"></div>
      </div>

      <ul
        v-if="canRenderLinks && !renderRouterLinks && !renderCustomLinks"
        :class="generateOpenClass"
      >
        <li v-for="link in config.links" :key="link.to" :class="renderCustomClass(config.liClass)">
          <a :href="link.to" :class="renderCustomClass(config.aClass)" v-if="link.icon">
            <component :is="link.icon()" />
            {{ link.value }}
          </a>
          <a :href="link.to" :class="renderCustomClass(config.aClass)" v-else>{{ link.value }}</a>
        </li>
      </ul>
      <ul v-else-if="canRenderLinks && renderRouterLinks" :class="generateOpenClass">
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
    </div>
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
    },
    navbarIsOpen() {
      return this.config.mobileMode ? "open" : undefined;
    },
    handleMenuClick() {
      this.$emit("menu-click");
    }
  },
  computed: {
    renderCustomLinks() {
      return typeof this.config.customLinksComponent === "function";
    },
    renderRouterLinks() {
      return this.config.useAnchor === false;
    },
    generateOpenClass() {
      const defaultClass = this.renderCustomClass(
        this.config.ulClass,
        "nav-links"
      );
      const navbarIsOpen = this.navbarIsOpen() ? " " + this.navbarIsOpen() : "";
      return defaultClass + navbarIsOpen;
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
