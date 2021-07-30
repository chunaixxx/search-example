<template>
	<header class="header">
		<div class="header__inner">
			<a href="#" class="logo">chunai</a>

			<div class="social-links">
				<a
					class="social-links__link"
					href="https://t.me/chunaichunai"
					target="_blank"
				>
					<img
						class="social-links__icon"
						src="./assets/telegram-icon.svg"
						alt=""
					/>
				</a>

				<a
					class="social-links__link"
					href="https://github.com/chunaixxx"
					target="_blank"
				>
					<img
						class="social-links__icon"
						src="./assets/github-icon.svg"
						alt=""
					/>
				</a>
			</div>
		</div>

		<search-input class="search" v-model.trim="search" />
	</header>

	<main class="cards">
		<img
			v-if="isLoading"
			class="preloader"
			src="./assets/preloader.svg"
			alt=""
		/>

		<transition-group v-else name="users">
			<user-card
				v-for="user in searchedUsers"
				class="card"
				:user="user"
				:key="user.login.uuid"
			/>
		</transition-group>
	</main>
</template>

<script>
import SearchInput from '@/components/SearchInput'
import UserCard from '@/components/UserCard'

export default {
	components: {
		SearchInput,
		UserCard
	},

	data: () => ({
		isLoading: true,
		search: '',

		users: []
	}),

	computed: {
		searchedUsers() {
			return this.users.filter(user => {
				const name = (user.name.first + ' ' + user.name.last).toLowerCase()

				return name.includes(this.search.toLowerCase())
			})
		}
	},

	async mounted() {
		try {
			const response = await fetch('https://randomuser.me/api/?results=70&inc=name,picture,login,email,phone&nat=us&noinfo')
			const data = await response.json()
			this.users = data.results
		} catch (e) {
			console.log(e)
		} finally {
			this.isLoading = false
		}
	}
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
	height: 100px;
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
	font-size: 1.3em;
}

.social-links {
	display: flex;
	gap: 15px;

	&__icon {
		width: 25px;
	}
}

.cards {
	padding: 50px;

	display: grid;
	grid-template-columns: 1fr 1fr 1fr;
	gap: 40px;
}

.preloader {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}

.card {
	height: 130px;
}

.users-enter-active,
.users-leave-active {
	transition: all 1s ease;
}
.users-enter-from,
.users-leave-to {
	opacity: 0;
	transform: translateY(0px);
}
</style>
