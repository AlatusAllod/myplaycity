<template>
  <aside :class="$style['aside-menu']">
    <header :class="$style.header">
      <img :class="$style.avatar" src="../assets/img/avatar.jpg" alt="David Hill">
      <div :class="$style.info">
        <h4 :class="$style.title">David Hill</h4>
        <p :class="$style.subtitle">online</p>
      </div>
      <button :class="$style['button-add']"></button>
    </header>
    <main :class="$style.groups">
      <h4 :class="$style.title">MESSAGES</h4>
      <p :class="$style.subtitle">history</p>
      <menu :class="$style.groups">
        <asideList v-for="value in uniqueCategories" :key="value" :data="value" :issues="issues"></asideList>
      </menu>
      <button :class="$style['add-category']" @click="addCategory">+ Add Category</button>
    </main>
  </aside>
</template>

<script>
import asideList from "./aside-list";

export default {
  data() {
    return {
      defaultCategories: ["My Questions", "Messenger", "Community QA", "FAQ"]
    };
  },
  props: {
    issues: Array
  },
  components: {
    asideList
  },
  computed: {
    uniqueCategories() {
      const set = new Set();
      this.issues.forEach(elem => {
        set.add(elem.categoryName);
      });
      this.defaultCategories.forEach(elem => set.add(elem));
      return [...set];
    }
  },
  methods: {
    addCategory() {
      this.defaultCategories.push("Unnamed category");
    }
  }
};
</script>

<style lang="sass" module>
	.aside-menu
		/* Display & Box Model */
		min-height: 100vh
		height: 100%
		width: 300px
		padding: 20px
		background-color: rgb(3, 33, 41)

		/* Positioning */
		position: fixed
		z-index: 1

		/* Other */
		overflow-y: auto
	.header
		/* Display & Box Model */
		display: flex
		align-items: center
		padding-bottom: 20px
		margin-bottom: 10px

		/* Positioning */
		position: relative
		&::after
			/* Display & Box Model */
			content: ''
			width: 100%
			height: 1px
			background: linear-gradient(to left, rgba(white ,.1) 0%, rgba(white ,.3) 50%, rgba(white ,.1) 100%)

			/* Positioning */
			position: absolute
			bottom: 0
	.avatar
		/* Display & Box Model */
		width: 50px
		height: 50px
		object-fit: cover
		border-radius: 10px
		margin-right: 10px
	.info
		/* Display & Box Model */
		flex: 1
	.title
		/* Display & Box Model */
		margin-top: 0
		margin-bottom: 5px

		/* Text */
		font-weight: bold
		color: white
	.subtitle
		/* Display & Box Model */
		margin-top: 0
		margin-bottom: 0

		/* Text */
		font-size: 0.8rem
		color: rgba(white, 0.2)
	.button-add
		/* Display & Box Model */
		width: 30px
		height: 30px
		padding: 0
		border: none
		border-radius: 50%
		background-color: rgba(white, 0.2)

		/* Positioning */
		position: relative

		/* Other */
		cursor: pointer
		transition: transform .5s
		&:hover,
		&:focus
			/* Display & Box Model */
			transform: rotate(180deg) scale(1.1)
		&::after,
		&::before
			/* Display & Box Model */
			content: ''
			height: 60%
			width: 5px
			background-color: rgb(3, 33, 41)
			border-radius: 5px
			transform: translate(-50%, -50%)

			/* Positioning */
			position: absolute
			top: 50%
			left: 50%
		&::before
			/* Display & Box Model */
			transform: translate(-50%, -50%) rotate(90deg)
	.groups
		/* Display & Box Model */
		padding: 0
	.add-category
		/* Display & Box Model */
		padding: 0
		border: none
		background-color: transparent

		/* Text */
		color: rgba(white, .5)

		/* Other */
		cursor: pointer
		&:hover,
		&:focus
			/* Display & Box Model */
			color: white
</style>
