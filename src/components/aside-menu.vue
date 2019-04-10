<template>
  <aside :class="$style['aside-menu']">
    <header :class="$style.header">
      <img :class="$style.avatar" src="../assets/img/avatar.jpg" alt="David Hill">
      <div :class="$style.info">
        <h4 :class="$style.username">David Hill</h4>
        <p :class="$style.status">online</p>
      </div>
      <button :class="$style['button-add']"></button>
    </header>
  </aside>
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
		width: 300px
		padding: 20px
		background-color: rgb(3, 33, 41)

		/* Positioning */
		position: fixed
	.header
		/* Display & Box Model */
		display: flex
		align-items: center
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
	.username
		/* Display & Box Model */
		margin-top: 0
		margin-bottom: 5px

		/* Text */
		font-weight: bold
		color: white
	.status
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
			
			/* Other */
			cursor: pointer
		&::before
			/* Display & Box Model */
			transform: translate(-50%, -50%) rotate(90deg)
</style>
