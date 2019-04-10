<template>
  <section :class="$style.section">
    <asideMenu></asideMenu>
  </section>
</template>

<script>
import asideMenu from "./components/aside-menu";

export default {
  name: "app",
  components: {
    asideMenu
  }
};
</script>

<style lang="sass" module>
  .section
    /* Display & Box Model */
    display: flex
    min-height: 100vh
    width: 100vw
</style>
