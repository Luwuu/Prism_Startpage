<template>
	<div class="search">
		<div class="search__thread search__thread"></div>
		<input
			@focus="$emit('disableHotkeys')"
			@blur="$emit('enableHotkeys')"
			type="text"
			class="search__bar"
			placeholder="Search"
			autofocus
			autocomplete="on"
		/>
	</div>
</template>

<script>
export default {
	emits: ['diableHotkeys', 'enableHotkeys'],
	mounted() {
		//Arbitrary Code copied from some repo, will not worry about edit till later
		String.prototype.replaceChars = function(character, replacement) {
			let str = this
			let a
			let b
			for (let i = 0; i < str.length; i++) {
				if (str.charAt(i) == character) {
					a = str.substr(0, i) + replacement
					b = str.substr(i + 1)
					str = a + b
				}
			}
			return str
		}

		function search(query) {
			switch (query.substr(0, 2)) {
				case '-g':
					query = query.substr(3)
					window.location =
						'https://www.google.fr/search?q=' +
						query.replaceChars(' ', '+')
					break

				case '-r':
					query = query.substr(3)
					window.location =
						'https://www.reddit.com/search?q=' +
						query.replaceChars(' ', '+')
					break

				case '-y':
					query = query.substr(3)
					window.location =
						'https://www.youtube.com/results?search_query=' +
						query.replaceChars(' ', '+')
					break

				case '-k':
					query = query.substr(3)
					window.location =
						'https://kissanime.ru/Anime/' +
						query.replaceChars(' ', '%20')
					break
				default:
					window.location =
						'https://duckduckgo.com/?q=' +
						query.replaceChars('', '+')
			}
		}

		// search
		const searchinput = document.querySelector('.search__bar')
		if (searchinput) {
			searchinput.addEventListener('keypress', function(event) {
				let key = event.keyCode
				if (key == 13) {
					let query = this.value
					search(query)
				}
			})
		}
	},
	methods: {},
}
</script>

<style lang="scss">
.search {
	position: absolute;
	width: 80vw;
	max-width: 80rem;
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
