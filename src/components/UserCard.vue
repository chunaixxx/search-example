<template>
	<div class="card">
		<img class="card__picture" :src="user.picture.large" alt="">

		<div class="card__inner">
			<div class="card__info">
				<h3 class="card__name">{{ user.name.first }} {{ user.name.last }}</h3>
				<h4 class="card__username">@{{ user.login.username }}</h4>
			</div>

			<div class="card__contacts">
				<a :href="'tel:' + user.phone" class="card__link card__phone">
					<img class="card__icon" src="../assets/phone-icon.svg" alt="">
					<span>{{ user.phone }}</span>
				</a>
				<a :href="'mailto:' + user.email" class="card__link card__email">
					<img class="card__icon" src="../assets/email-icon.svg" alt="">
					
					<span :title="user.email">
						{{ user.email.length > 20 ? user.email.slice(0, 20) + '...' : user.email }}
					</span>
				</a>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'UserCard',
	props: {
		user: {
			name: {
				first: String,
				last: String,
			},

			login: {
				username: String,
			},

			picture: {
				large: String,
			},

			phone: String,
			email: String
		}
	}
}
</script>

<style lang="scss" scoped>
.card {
	background-color: #fff;
	box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
	border-right: 3px solid #4169e1;

	display: flex;

	&__picture {
		height: 100%;
	}

	&__inner {
		padding: 15px;
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	&__name {
		color: #333;
		font-weight: 500;
	}

	&__username {
		color: #666;
		font-weight: 400;
	}

	&__contacts {
		font-size: .8em;
		display: flex;
		flex-direction: column;
		gap: 5px;
	}

	&__link {
		display: flex;
		align-items: center;
	}

	&__icon {
		width: 13px;
		margin-right: 5px;
	}
}
</style>