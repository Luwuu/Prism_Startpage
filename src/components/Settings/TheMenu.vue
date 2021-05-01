<template>
	<section class="menu" :class="{ hidden: activeMenu }">
		<div class="menu__icon">
			<i
				v-if="!activeMenu"
				@click="activeMenu = true"
				class="menu__icon fas fa-sliders-h"
			></i>
			<i
				v-else
				@click="activeMenu = false"
				class="menu__icon fas fa-times"
			></i>
		</div>
		<div v-if="activeMenu" class="menu__content">
			<TheHotkeys />
			<div class="menu__settings">
				<div class="menu__settings--image">
					<label for="image">Image</label>
					<input
						type="text"
						placeholder="https://imageUrl.jpg"
						ref="image"
						:value="imageUrl"
					/>
				</div>
				<div class="menu__settings--image">
					<label for="image">Primary Color</label>
					<input
						type="text"
						placeholder="rgb | hsl | hex"
						ref="primaryColor"
						:value="primaryColor"
					/>
				</div>
				<div class="menu__settings--image">
					<label for="image">Text Color</label>
					<input
						type="text"
						placeholder="rgb | hsl | hex"
						ref="textColor"
						:value="textColor"
					/>
				</div>
				<div class="menu__settings--image">
					<label for="image">Background Color</label>
					<input
						type="text"
						placeholder="rgb | hsl | hex"
						ref="bgColor"
						:value="bgColor"
					/>
				</div>

				<div class="menu__settings--links">
					<label for="links">Links</label>
					<textarea
						name="links"
						:value="linksExample"
						spellcheck="false"
						ref="config"
					></textarea>
				</div>
				<div class="menu__options">
					<button @click="saveAndCloseMenu" class="btn">
						Save & Close
					</button>
					<button @click="closeMenu" class="btn">Close</button>
				</div>
			</div>
		</div>
	</section>
</template>

<script>
import TheHotkeys from "@/components/Settings/TheHotkeys"
export default {
	emits: ["hideContent", "showContent", "refreshComponent"],
	components: {
		TheHotkeys,
	},
	data() {
		return {
			imageUrl:
				localStorage.getItem("image") ||
				"https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/a62b63a0-c6c7-4d49-8331-000bbca6d366/dbgryze-d07f5c26-5704-40d8-810a-beff011d3830.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcL2E2MmI2M2EwLWM2YzctNGQ0OS04MzMxLTAwMGJiY2E2ZDM2NlwvZGJncnl6ZS1kMDdmNWMyNi01NzA0LTQwZDgtODEwYS1iZWZmMDExZDM4MzAuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.icZkv2-SPq5mG8-NZBFbuc_JUSgV0bB8BrNA1BA-BmM",
			primaryColor: localStorage.getItem("primaryColor") ?? "#b9878a",
			textColor: localStorage.getItem("textColor") ?? "#fff",
			bgColor: localStorage.getItem("bgColor") ?? "#6e5d80",

			activeMenu: false,
			linksExample:
				localStorage.getItem("config") ||
				`
[
    {
		"category": "Anime",
		"links": [
			["wallpapers", "https://wallhaven.cc"],
			["nyaa", "https://nyaa.si"],
			["animepahe", "https://animpahe.com"],
			["animelist", "https://nippah.com/user/kaiandlulu"]
		]
	},
	{
		"category": "Social",
		"links": [
			["YouTube", "https://youtube.com"],
			["Reddit", "https://reddit.com"],
			["Twitter", "https://twitter.com"]
		]
	},
	{
		"category": "Programming",
		"links": [
			["Github", "https://github.com"],
			["StackOverflow", "https://stackoverflow.com"],
			["Codepen", "https://codepen.io"],
			["CodinGame", "https://codingame.com"],
			["W3 Schools", "https://w3schools.com"],
			["Vue Docs", "https://v3.vuejs.org/"]
		]
	},
	{
		"category": "Misc.",
		"links": [
			["YouTube", "https://wallhaven.cc"],
			["Reddit", "https://nyaa.si"],
			[
				"Artist Art Page",
				"https://www.deviantart.com/fadocanslap/gallery?catpath=%2F&sort=popularity"
			]
		]
	}
]
`,
		}
	},
	watch: {
		activeMenu(status) {
			if (status) this.$emit("hideContent")
			else this.$emit("showContent")
		},
	},
	methods: {
		closeMenu() {
			this.activeMenu = false
		},
		saveAndCloseMenu() {
			localStorage.setItem("config", this.$refs.config.value)
			localStorage.setItem("image", this.$refs.image.value)
			localStorage.setItem("primaryColor", this.$refs.primaryColor.value)
			localStorage.setItem("textColor", this.$refs.textColor.value)
			localStorage.setItem("bgColor", this.$refs.bgColor.value)

			this.closeMenu()
			this.$emit("refreshComponent")
		},
	},
}
</script>

<style lang="scss" scoped>
.menu {
	z-index: 2000;
	position: absolute;
	top: 0;
	right: 0;
	height: 100%;
	display: flex;
	flex-direction: column;
	align-items: flex-start;
	padding: 1rem;
	color: var(--text-color);
	&__content {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		width: 60vw;
		height: 100%;
		border: 2px solid var(--primary-color);
		border-radius: 0.5rem;
		padding: 1rem;
		overflow: scroll;
	}
	&__icon {
		cursor: pointer;
		font-size: 3rem;
		color: var(--primary-color);
		opacity: 0.8;
		align-self: flex-end;
	}
	&__options {
		margin: 1rem 0;
		width: 100%;
		button {
			cursor: pointer;
			margin-right: 1rem;
			border: none;
			padding: 0.5rem 1rem;
			border-radius: 0.5rem;
			background: var(--primary-color);
			color: var(--text-color);
			border-bottom: 1px solid var(--text-color);
		}
	}
	&__settings {
		width: 100%;
		height: 30rem;
		font-size: 1.4rem;
		&--image {
			margin-bottom: 0.5rem;
			input {
				border: none;
				background: var(--primary-color);
				color: var(--text-color);
				padding: 0.5rem;
				border-radius: 0.5rem;
				margin-left: 1rem;
			}
		}
		&--links,
		&--image {
			width: 100%;
			textarea {
				display: block;
				background: var(--primary-color);
				color: var(--text-color);
				font-weight: 600;
				width: 100%;
				height: 65vh;
				max-height: 80vh;
				border: none;
				border-radius: 0.5rem;
				opacity: 0.95;
				&:focus {
					outline: var(--text-color);
				}
			}
		}
	}
}
</style>
