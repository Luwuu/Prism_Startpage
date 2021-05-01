<template>
	<SearchBar />
	<MainContent />
</template>

<script>
import SearchBar from '@/components/SearchBar.vue'
import MainContent from '@/components/MainContent.vue'
export default {
	components: {
		SearchBar,
		MainContent,
	},
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,300;0,400;0,500;0,600;0,700;1,200;1,300&display=swap');
:root {
	--primary-color: #40b992;
	--text-color: #fff;
	--bg-color: #ad4727;
}

html {
	font-size: 62.5%;
}

* {
	box-sizing: border-box;
	margin: 0;
}

body {
	background: var(--bg-color);
	font-family: 'Poppins', sans-serif;
}

#app {
	width: 100vw;
	height: 100vh;
	display: grid;
	place-items: center;
}
</style>
