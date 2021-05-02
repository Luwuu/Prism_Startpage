<template>
	<div @click="searchVisible = false" class="overlay"></div>
	<transition name="search">
		<SearchBar
			v-if="searchVisible"
			@enableHotkeys="hotkeys = true"
			@disableHotkeys="hotkeys = false"
		/>
	</transition>
	<div class="card">
		<div class="card__backdrop" ref="card"></div>
		<div class="card__content" ref="content">
			<div
				v-if="mode === 0"
				class="card__image"
				:style="{ backgroundImage: `url(${image})` }"
			>
				<div
					class="card__image--backdrop"
					:style="{ backgroundImage: `url(${image})` }"
				></div>
			</div>
			<div v-else @click="mode = 0" class="links">
				<h5 class="links__category">{{ activeCategory.category }}</h5>
				<a
					:href="link[1]"
					v-for="link in activeCategory.links"
					:key="link[0]"
					class="links__link .btn-text"
					>{{ link[0] }}</a
				>
			</div>
		</div>
		<div
			@click="mode = 1"
			class="tab tab--1"
			:class="{ underline: mode == 1 }"
		>
			I
		</div>
		<div
			@click="mode = 2"
			class="tab tab--2"
			:class="{ underline: mode == 2 }"
		>
			II
		</div>
		<div
			@click="mode = 3"
			class="tab tab--3"
			:class="{ underline: mode == 3 }"
		>
			III
		</div>
		<div
			@click="mode = 4"
			class="tab tab--4"
			:class="{ underline: mode == 4 }"
		>
			IV
		</div>
	</div>
</template>

<script>
import VanillaTilt from "vanilla-tilt"
import SearchBar from "@/components/Homepage/SearchBar.vue"

export default {
	components: {
		SearchBar,
	},
	data() {
		return {
			searchVisible: false,
			hotkeys: true,
			image:
				localStorage.getItem("image") ||
				"https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/a62b63a0-c6c7-4d49-8331-000bbca6d366/dbgryze-d07f5c26-5704-40d8-810a-beff011d3830.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcL2E2MmI2M2EwLWM2YzctNGQ0OS04MzMxLTAwMGJiY2E2ZDM2NlwvZGJncnl6ZS1kMDdmNWMyNi01NzA0LTQwZDgtODEwYS1iZWZmMDExZDM4MzAuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.icZkv2-SPq5mG8-NZBFbuc_JUSgV0bB8BrNA1BA-BmM",
			// MODES
			// 0 - image - fade-in
			// 1 - tab 1 - slide from top
			// 2 - tab 2 - slide from bottom
			// 3 - tab 3 - slide from right
			// 4 - tab 4 - slide from left
			mode: 0,
			config: [],
			activeCategory: {},
		}
	},
	mounted() {
		//Change Colorscheme if user config permits
		if (localStorage.getItem("primaryColor"))
			document.documentElement.style.setProperty(
				"--primary-color",
				localStorage.getItem("primaryColor")
			)
		if (localStorage.getItem("textColor"))
			document.documentElement.style.setProperty(
				"--text-color",
				localStorage.getItem("textColor")
			)
		if (localStorage.getItem("bgColor"))
			document.documentElement.style.setProperty(
				"--bg-color",
				localStorage.getItem("bgColor")
			)
		this.config = JSON.parse(localStorage.getItem("config")) || [
			//Mode 1
			{
				category: "Anime",
				links: [
					["wallpapers", "https://wallhaven.cc"],
					["nyaa", "https://nyaa.si"],
					["animepahe", "https://animpahe.com121"],
					["animelist", "https://nippah.com/user/kaiandlulu"],
				],
			},
			//Mode 2
			{
				category: "Social",
				links: [
					["YouTube", "https://youtube.com"],
					["Reddit", "https://reddit.com"],
					["Twitter", "https://twitter.com"],
				],
			},
			//Mode 3
			{
				category: "Programming",
				links: [
					["Github", "https://github.com"],
					["StackOverflow", "https://stackoverflow.com"],
					["Codepen", "https://codepen.io"],
					["CodinGame", "https://codingame.com"],
					["W3 Schools", "https://w3schools.com"],
					["Vue Docs", "https://v3.vuejs.org/"],
				],
			},
			//Mode 4
			{
				category: "Misc.",
				links: [
					["YouTube", "https://wallhaven.cc"],
					["Reddit", "https://nyaa.si"],
					[
						"Artist Art Page",
						"https://www.deviantart.com/fadocanslap/gallery?catpath=%2F&sort=popularity",
					],
				],
			},
		]
		//Setup Key Event
		document.addEventListener("keydown", (event) => {
			if (this.hotkeys) {
				switch (event.key) {
					case "0":
					case "`":
					case "5":
						this.mode = 0
						break
					case "1":
						this.mode = 1
						break
					case "2":
						this.mode = 2
						break
					case "3":
						this.mode = 3
						break
					case "4":
						this.mode = 4
						break
					case "s":
					case " ":
						this.mode = 0
						this.searchVisible = !this.searchVisible
						break
				}
			}
		})
		//Vanilla Tilt
		this.activateTilt()
	},
	watch: {
		mode() {
			this.updateMode()
			this.animateContent()
		},
	},
	methods: {
		activateTilt() {
			VanillaTilt.init(document.querySelector(".card__content"), {
				max: 25,
				speed: 400,
			})
		},
		removeTilt() {
			this.$refs.content.vanillaTilt?.destroy()
		},
		animateContent() {
			this.$refs.card.classList.add("animate--rotate")
			this.$refs.content.classList.add("animate--fadeIn")

			const animationTime = 300 //ms
			setTimeout(() => {
				this.$refs.card.classList.remove("animate--rotate")
				this.$refs.content.classList.remove("animate--fadeIn")
			}, animationTime)
		},
		updateMode() {
			switch (this.mode) {
				case 0:
					this.activateTilt()
					break
				case 1:
				case 2:
				case 3:
				case 4:
					this.activeCategory = this.config[this.mode - 1]
					this.removeTilt()
					break
			}
		},
	},
}
</script>

<style lang="scss" scoped>
@keyframes rotate {
	from {
		transform: rotate(0deg);
	}
	to {
		transform: rotate(360deg);
	}
}

@keyframes fadeIn {
	from {
		opacity: 0;
	}
	to {
		opacity: 1;
	}
}

@keyframes slideInFromTop {
	from {
		transform: translateY(-100%);
	}
	to {
		transform: translateY(0%);
	}
}

.overlay {
	position: fixed;
	left: 0;
	right: 0;
	bottom: 0;
	top: 0;
}

.search-enter-from {
	opacity: 0;
	transform: translateY(-30rem);
}

.search-enter-active {
	transition: all 0.3s ease-out;
}

.search-enter-to {
	opacity: 1;
	transform: translateY(0);
}

.search-leave-from {
	opacity: 1;
	transform: translateY(0);
}

.search-leave-active {
	transition: all 0.3s ease-in;
}

.search-leave-to {
	opacity: 0;
	transform: translateY(-30rem);
}

.underline {
	text-decoration: underline;
}

.animate {
	&--rotate {
		animation: rotate linear 0.3s forwards;
	}
	&--fadeIn {
		animation: fadeIn ease-out 0.3s forwards;
	}
}

.card {
	position: relative;
	width: 40rem;
	height: 40rem;
	border-radius: 0.5rem;
	&__backdrop,
	&__content {
		position: absolute;
		width: 100%;
		height: 100%;
		border-radius: 0.5rem;
	}
	&__backdrop {
		background: var(--primary-color);
		transform: rotate(45deg);
	}
	&__content {
		z-index: 100;
		background: var(--primary-color);
		box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
		perspective: 500px;
	}
	&__image {
		position: relative;
		width: 100%;
		height: 100%;
		border-radius: inherit;
		background-size: cover;
		background-position: top;
		background-repeat: no-repeat;
		&--backdrop {
			display: block;
			position: absolute;
			background: inherit;
			width: 100%;
			height: 100%;
			box-shadow: 0 10px 40px 0 rgba(76, 70, 124, 0.5);
			border-radius: inherit;
			z-index: -1;
			top: 3rem;
			transform: scale(0.9);
			filter: blur(1rem);
			opacity: 0.9;
		}
	}
}

.tab {
	--gap: -4rem;
	position: absolute;
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 2.4rem;
	color: var(--text-color);
	cursor: pointer;
	&--1 {
		width: 100%;
		top: var(--gap);
	}
	&--2 {
		width: 100%;
		bottom: var(--gap);
	}
	&--3 {
		height: 100%;
		right: var(--gap);
	}
	&--4 {
		height: 100%;
		left: var(--gap);
	}
}

.links {
	width: 100%;
	padding: 1rem;
	display: flex;
	align-items: center;
	flex-direction: column;
	color: var(--text-color);
	* {
		padding-bottom: 1.5rem;
	}
	&__category {
		font-size: 2.4rem;
	}
	&__link {
		position: relative;
		text-decoration: none;
		font-size: 1.6rem;
		color: var(--text-color);
		width: fit-content;
		text-align: center;
		&:after {
			content: "";
			position: absolute;
			left: 0;
			display: inline-block;
			height: 1em;
			width: 100%;
			border-bottom: 1px solid;
			margin-top: 10px;
			opacity: 0;
			transition: opacity 0.25s, transform 0.25s;
			transform: scale(0, 1);
		}

		&:hover:after {
			opacity: 1;
			transform: scale(1);
		}
	}
}

.btn {
	cursor: pointer;
	color: var(--text-color);
	position: absolute;
	bottom: 0.5rem;
	right: 0.5rem;
	border: none;
	background: transparent;
	border-radius: 0.3rem;
	text-decoration: underline;
}
</style>
