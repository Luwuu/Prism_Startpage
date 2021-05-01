<template>
	<div class="search">
		<div class="search__thread search__thread"></div>
		<input
			@focus="$emit('disableHotkeys')"
			@blur="$emit('enableHotkeys')"
			type="text"
			class="search__bar"
			placeholder="Search"
		/>
	</div>
</template>

<script>
export default {
	emits: ['diableHotkeys', 'enableHotkeys'],
}
</script>

<style lang="scss">
.search {
	position: absolute;
	width: 80vw;
	max-width: 100rem;
	display: flex;
	flex-direction: column;
	align-items: center;
	top: 0;
	&__bar {
		width: 100%;
		height: 5rem;
		z-index: 2000;
		border: 2px dotted var(--primary-color);
		font-size: 2rem;
		color: rgba(0, 0, 0, 0.6);
		font-family: poppins;
		padding-left: 1rem;
		border-radius: 0.5rem;
		box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
	}
	&__thread {
		z-index: 1000;
		width: 95%;
		height: 5rem;
		border-left: 2px dotted var(--primary-color);
		border-right: 2px dotted var(--primary-color);
	}
}
</style>
