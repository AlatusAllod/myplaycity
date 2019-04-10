<template>
  <aside :class="$style['aside-menu']"></aside>
</template>

<script>
export default {
  props: {
    asideMenu: Object
  }
};
</script>

<style lang="sass" module>
	.aside-menu
		/* Display & Box Model */
		height: 100vh
		width: 30%
		background-color: rgb(3, 33, 41)

		/* Positioning */
		position: fixed
</style>
