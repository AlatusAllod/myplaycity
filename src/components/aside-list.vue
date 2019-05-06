<template>
  <button :class="[$style.list, {[$style['list--active']]: isActive}]" @click="toggle">
    <img src="../assets/img/list-icon.png" alt="list">
    {{ data }}
    <template v-if="relevantIssues">({{ relevantIssues }})</template>
  </button>
</template>

<script>
import EventBus from "../main.js";

export default {
  data() {
    return {
      isActive: false,
      dataIssues: this.issues
    };
  },
  props: {
    data: String,
    issues: Array
  },
  computed: {
    relevantIssues() {
      return this.dataIssues.reduce(
        (acc, elem) => (elem.categoryName === this.data ? acc + 1 : acc),
        0
      );
    }
  },
  methods: {
    toggle() {
      EventBus.$emit("listDeactivate");
      this.isActive = true;
      EventBus.$emit("showIssues", this.data);
    }
  },
  mounted() {
    EventBus.$on("listDeactivate", () => {
      this.isActive = false;
    });
    EventBus.$on("addIssue", () => {
      this.dataIssues = JSON.parse(localStorage.issues, (key, value) =>
        key == "openDate" ? new Date(value) : value
      );
    });
  }
};
</script>

<style lang="sass" module>
	.list
		/* Display & Box Model */
		display: flex
		align-items: center
		width: 100%
		border: none
		border-radius: 4px
		padding: 5px
		background: none
		
		/* Text */
		color: rgba(white, .5)
		text-align: left

		/* Other */
		cursor: pointer
		&:hover,
		&:focus,
		&--active
			/* Display & Box Model */
			background-color: rgb(0, 126, 158)
			
			/* Text */
			color: white
		& img
			/* Display & Box Model */
			width: 15px
			margin-right: 5px
</style>
