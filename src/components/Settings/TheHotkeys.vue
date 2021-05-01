<template>
	<div class="card">
		<h3>Hotkeys</h3>
		<ul class="card__list">
			<li class="card__list-item">ImageScreen - 0 | 5 | ~</li>
			<li class="card__list-item">Show Search - Space | s</li>
			<li class="card__list-item">I - 1</li>
			<li class="card__list-item">II - 2</li>
			<li class="card__list-item">III - 3</li>
			<li class="card__list-item">IV - 4</li>
		</ul>
		<a href="https://github.com/Lu1uu/Prism_Startpage">
			<i class="fab fa-github"></i>
		</a>
	</div>
</template>

<style lang="scss" scoped>
.fab {
	color: var(--text-color);
	cursor: pointer;
	font-size: 2rem;
	float: right;
}

.card {
	width: 30rem;
	padding: 1rem;
	padding-left: 3rem;
	color: var(--text-color);
	background: var(--primary-color);
	border-radius: 0.5rem;
	font-size: 1.3rem;
	position: fixed;
	top: 5rem;
	left: 2rem;
}
</style>
