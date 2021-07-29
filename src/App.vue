<template>
	<header class="header">
		<div class="header__inner">
			<a href="#" class="logo">chunai</a>

			<div class="social-links">
				<a class="social-links__link" href="https://t.me/chunaichunai" target="_blank">
					<img
						class="social-links__icon"
						src="./assets/telegram-icon.svg"
						alt=""
					/>	
				</a>
				<a class="social-links__link" href="https://github.com/chunaixxx" target="_blank">
					<img
						class="social-links__icon"
						src="./assets/github-icon.svg"
						alt=""
					/>
				</a>
			</div>
		</div>

		<search-input class="search" v-model="search" />
	</header>
</template>

<script>
import SearchInput from '@/components/SearchInput'

export default {
	components: {
		SearchInput
	},

	data: () => ({
		search: ''
	})
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500;600;700&display=swap');

* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

a {
	color: inherit;
	text-decoration: none;
}

body {
	font-family: 'Montserrat', 'Arial', sans-serif;
	background-color: #eee;
}

.header {
	background-color: #4169e1;
	color: #fff;
	height: 150px;
	padding: 20px 50px 0 50px;

	display: flex;
	flex-direction: column;
	justify-content: space-between;

	&__inner {
		display: flex;
		justify-content: space-between;
		align-items: center;

		font-size: 1.2em;
	}
}

.logo {
	font-size: 1.3em;
}

.search {
	align-self: center;
	width: 80%;
	transform: translateY(50%);
	font-size: 1.6em;
}

.social-links {
	display: flex;
	gap: 15px;

	&__icon {
		width: 25px;
	}
}
</style>
