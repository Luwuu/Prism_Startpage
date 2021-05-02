<template>
	<TheMenu
		v-if="!refresh"
		@refreshComponent="refreshComponent"
		@showContent="showContent = true"
		@hideContent="showContent = false"
	/>
	<MainContent v-if="!refresh && showContent" />
</template>

<script>
import TheMenu from "@/components/Settings/TheMenu.vue"
import MainContent from "@/components/Homepage/MainContent.vue"
export default {
	components: {
		MainContent,
		TheMenu,
	},
	data() {
		return {
			refresh: false,
			showContent: true,
		}
	},
	methods: {
		refreshComponent() {
			this.refresh = true
			setTimeout(() => {
				this.refresh = false
			}, 200)
		},
	},
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,300;0,400;0,500;0,600;0,700;1,200;1,300&display=swap");
:root {
	--primary-color: #b9878a;
	--text-color: #fff;
	--bg-color: #6e5d80;
}

html {
	font-size: 62.5%;
}

* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	background: var(--bg-color);
	font-family: "Poppins", sans-serif;
}

#app {
	position: relative;
	width: 100vw;
	height: 100vh;
	display: grid;
	place-items: center;
}
</style>
