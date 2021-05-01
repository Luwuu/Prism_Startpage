<template>
	<div class="card">
		<h3>Hotkeys</h3>
		<ul class="card__list">
			<li class="card__list-item">0 | 5 | ~ - Image Screen</li>
			<li class="card__list-item">Space | s - Show Search</li>
			<li class="card__list-item">1 - I</li>
			<li class="card__list-item">2 - II</li>
			<li class="card__list-item">3 - III</li>
			<li class="card__list-item">4 - IV</li>
		</ul>
		<h3>Search Shortcuts</h3>
		<ul class="card__list">
			<li class="card__list-item">-g Google</li>
			<li class="card__list-item">-r Reddit</li>
			<li class="card__list-item">-y YouTube</li>
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
