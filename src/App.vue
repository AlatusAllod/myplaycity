<template>
  <section :class="$style.section">
    <asideMenu :issues="issues"></asideMenu>
    <messageBoard :issues="issues"></messageBoard>
  </section>
</template>

<script>
import asideMenu from "./components/aside-menu";
import messageBoard from "./components/message-board";

export default {
  name: "app",
  components: {
    asideMenu,
    messageBoard
  },
  created() {
    if (!localStorage.issues) {
      localStorage.issues = JSON.stringify([
        {
          categoryName: "My Questions",
          id: "Q2718",
          openDate: new Date("05.02.2019 12:46"),
          isOpen: false,
          issue: "lorem ipsum"
        },
        {
          categoryName: "My Questions",
          id: "Q2719",
          openDate: new Date("05.02.2019 13:42"),
          isOpen: true,
          issue: "lorem ipsum lorem"
        },
        {
          categoryName: "My Questions",
          id: "Q2721",
          openDate: new Date("05.02.2019 12:46"),
          isOpen: false,
          issue: "lorem ipsum"
        },
        {
          categoryName: "My Questions",
          id: "Q2722",
          openDate: new Date("05.02.2019 13:42"),
          isOpen: true,
          issue: "lorem ipsum lorem"
        },
        {
          categoryName: "Messenger",
          id: "Q2720",
          openDate: new Date("04.02.2019 22:12"),
          isOpen: false,
          issue: "lorem ipsum lorem"
        }
      ]);
    }
    this.issues = JSON.parse(localStorage.issues, (key, value) =>
      key == "openDate" ? new Date(value) : value
    );
  }
};
</script>

<style lang="sass" module>
	*
		/* Display & Box Model */
		box-sizing: border-box
	body
		font-family: 'Roboto', sans-serif
	.section
		/* Display & Box Model */
		display: flex
		min-height: 100vh
		width: 100vw
</style>
