<template>
  <section :class="$style.container">
    <header :class="$style.header">
      <h4 :class="$style.title">{{ activeCategory || 'Questions'}}</h4>
      <button :class="$style['all-questions']">All Questions</button>
    </header>
    <main :class="$style.board">
      <message v-for="value in activeIssues" :key="value.id" :data="value"></message>
    </main>
    <footer v-if="activeCategory" :class="$style.footer">
      <form @submit="addIssue">
        <textarea></textarea>
        <button>Submit</button>
      </form>
    </footer>
  </section>
</template>

<script>
import message from "./message";
import EventBus from "../main.js";

export default {
  data() {
    return {
      activeCategory: null,
      dataIssues: this.issues
    };
  },
  props: {
    issues: Array
  },
  components: {
    message
  },
  computed: {
    activeIssues() {
      return this.dataIssues.filter(
        elem => elem.categoryName === this.activeCategory
      );
    }
  },
  methods: {
    addIssue(event) {
      event.preventDefault();
      this.dataIssues.push({
        categoryName: this.activeCategory,
        id: "Q" + Math.floor(Math.random() * (9000 - 3000) + 3000),
        openDate: new Date(),
        isOpen: true,
        issue: event.target[0].value
      });
      event.target[0].value = "";
      localStorage.issues = JSON.stringify(this.dataIssues);
      EventBus.$emit("addIssue");
    }
  },
  mounted() {
    EventBus.$on("showIssues", activeCategory => {
      this.activeCategory = activeCategory;
    });
  }
};
</script>

<style lang="sass" module>
	.container
		/* Display & Box Model */
		min-height: 100vh
		width: 100vw
		margin-left: 300px

		/* Positioning */
		position: relative
	.header
		/* Display & Box Model */
		display: flex
		flex-direction: column
		align-items: flex-start
		justify-content: space-between
		height: 90px
		padding: 20px
		background-color: white
		box-shadow: 0px 0px 8px -3px rgba(0,0,0,0.75)

		/* Positioning */
		position: fixed
		top: 0
		left: 300px
		right: 0
		z-index: 1
	.title
		/* Display & Box Model */
		margin: 0
		opacity: .7

		/* Text */
		font-size: 20px

	.all-questions
		/* Display & Box Model */
		padding: 0
		padding-right: 15px
		border: none
		opacity: .3

		/* Positioning */
		position: relative

		/* Text */
		font-weight: bold

		/* Other */
		cursor: pointer
		&::after
			/* Display & Box Model */
			content: ""
			border-style: solid
			border-width: 5px 5px 0 5px
			border-color: black transparent transparent transparent
			transform: translateY(-50%)

			/* Positioning */
			position: absolute
			top: 50%
			right: 0
	.board
		/* Display & Box Model */
		min-height: 100%
		padding: 110px 20px 100px
		background-color: rgb(216, 232, 241)
	.footer
		/* Display & Box Model */
		height: 100px
		width: calc(100% - 300px)
		padding: 10px
		background-color: white
		box-shadow: 0px 0px 8px -3px rgba(0,0,0,0.75)

		/* Positioning */
		position: fixed
		bottom: 0
		left: 300px
		form
			/* Display & Box Model */
			display: flex
			align-items: flex-end
			width: 100%
			height: 100%
		textarea
			/* Display & Box Model */
			flex-grow: 1
			height: 100%
			padding: 5px
			margin-right: 10px
			resize: none
			border-radius: 4px
		button
			/* Display & Box Model */
			padding: 5px 20px
			background-color: transparent
			border: 1px solid #032129
			border-radius: 4px

			/* Text */
			color: #032129

			/* Other */
			cursor: pointer
</style>
