<template>
	<section class="menu">
		<i class="menu__icon fas fa-sliders-h"></i>
	</section>
</template>

<script>
export default {}
</script>

<style lang="scss">
.menu {
	z-index: 2000;
	position: absolute;
	top: 1rem;
	right: 2rem;
	&__icon {
		cursor: pointer;
		font-size: 3rem;
		color: var(--primary-color);
	}
}
</style>
