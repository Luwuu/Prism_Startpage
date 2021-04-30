<template>
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
			<div v-else class="links">
				<h5 class="links__category">{{ category.category }}</h5>
				<a
					:href="link[1]"
					v-for="link in category.links"
					:key="link[0]"
					class="links__link"
					>{{ link[0] }}</a
				>
				<button @click="mode = 0" class="btn">Back to image</button>
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
import VanillaTilt from 'vanilla-tilt'
export default {
	data() {
		return {
			image:
				'https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/a62b63a0-c6c7-4d49-8331-000bbca6d366/deculn3-7d953a40-f478-410c-a549-642cce6d8cfb.png/v1/fill/w_896,h_891,strp/aw_by_fadocanslap_deculn3-pre.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7ImhlaWdodCI6Ijw9MTI3MyIsInBhdGgiOiJcL2ZcL2E2MmI2M2EwLWM2YzctNGQ0OS04MzMxLTAwMGJiY2E2ZDM2NlwvZGVjdWxuMy03ZDk1M2E0MC1mNDc4LTQxMGMtYTU0OS02NDJjY2U2ZDhjZmIucG5nIiwid2lkdGgiOiI8PTEyODAifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6aW1hZ2Uub3BlcmF0aW9ucyJdfQ.6v3a1NdxqM3DawevnATeaZMVOau92JbQxGvNrhtpYxw',
			// MODES
			// 0 - image - fade-in
			// 1 - tab 1 - slide from top
			// 2 - tab 2 - slide from bottom
			// 3 - tab 3 - slide from right
			// 4 - tab 4 - slide from left
			mode: 0,
			config: [
				//Mode 1
				{
					category: 'Anime',
					links: [
						['wallpapers', 'https://wallhaven.cc'],
						['nyaa', 'https://nyaa.si'],
					],
				},
				//Mode 2
				{
					category: 'Social',
					links: [
						['YouTube', 'https://wallhaven.cc'],
						['Reddit', 'https://nyaa.si'],
					],
				},
				//Mode 3
				{
					category: 'Programming',
					links: [
						['YouTube', 'https://wallhaven.cc'],
						['Reddit', 'https://nyaa.si'],
					],
				},
				//Mode 4
				{
					category: 'Misc.',
					links: [
						['YouTube', 'https://wallhaven.cc'],
						['Reddit', 'https://nyaa.si'],
					],
				},
			],
			category: {},
		}
	},
	mounted() {
		this.updateMode()
		//Setup Key Event
		document.addEventListener('keydown', (event) => {
			this.mode = event.key == '`' ? 0 : +event.key
		})
		//Vanilla Tilt
		VanillaTilt.init(document.querySelector('.card__content'), {
			max: 25,
			speed: 400,
		})
	},
	watch: {
		mode() {
			this.updateMode()
			this.animateContent()
		},
	},
	methods: {
		checkKeyPress(key) {
			alert(key)
		},
		animateContent() {
			this.$refs.card.classList.add('animate--rotate')
			this.$refs.content.classList.add('animate--fadeIn')

			const animationTime = 300 //ms
			setTimeout(() => {
				this.$refs.card.classList.remove('animate--rotate')
				this.$refs.content.classList.remove('animate--fadeIn')
			}, animationTime)
		},
		updateMode() {
			switch (this.mode) {
				case 1:
					this.category = this.config[0]
					break
				case 2:
					this.category = this.config[1]
					break
				case 3:
					this.category = this.config[2]
					break
				case 4:
					this.category = this.config[3]
					break
			}
		},
	},
}
</script>

<style lang="scss">
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
		margin-bottom: 1rem;
	}
	&__category {
		font-size: 2.4rem;
	}
	&__link {
		font-size: 1.6rem;
		color: var(--text-color);
		text-decoration: none;
		border-bottom: 1px dotted var(--text-color);
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
	border-left: 2px dotted var(--text-color);
	border-top: 2px dotted var(--text-color);
}
</style>
