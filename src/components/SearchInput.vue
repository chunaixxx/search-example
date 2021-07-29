<template>
	<div class="search">
		<input
			class="search__input"
			type="text"
			placeholder="Search..."

			:value="modelValue"
			@input="updateValue"

			ref="input"
		/>

		<div class="search__border"></div>

		<button class="search__button search__cancel-btn" @mousedown="clearInput">
			<img
				class="search__icon search__icon-cancel"
				src="../assets/cancel-icon.svg"
				alt=""
			/>
		</button>
		
		<button class="search__button search__search-btn" @click="focus">
			<img
				class="search__icon search__icon-search"
				src="../assets/search-icon.svg"
				alt=""
			/>
		</button>


	</div>
</template>

<script>
export default {
	name: 'SearchInput',
	emits: ['update:modelValue'],

	props: {
		modelValue: String
	},

	methods: {
		focus() {
			this.$refs.input.focus()
		},

		clearInput() {
			this.$emit('update:modelValue', '')
		},

		updateValue(e) {
			this.$emit('update:modelValue', e.target.value)
		}
	}
}
</script>

<style lang="scss" scoped>
.search {
	position: relative;
	border-radius: 5px;
	overflow: hidden;

	box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;

	&__input {
		padding: 12px 50px 12px 20px;
		width: 100%;

		color: #333;
		font-family: 'Montserrat', 'Arial', sans-serif;
		font-weight: 300;
		font-size: inherit;

		border: none;
		outline: none;

		&::placeholder {
			color: #666;
		}

		&:focus + .search__border {
			transform: rotateX(0deg);
			background-color: #4169e1;
		}

		&:focus ~ .search__cancel-btn {
			transform: scale(1);
		}

		&:focus ~ .search__search-btn {
			transform: scale(0);
		}
	}

	&__border {
		position: absolute;
		background-color: #333;
		left: 0;
		bottom: 0;
		transition: all 0.25s ease;
		transform: rotateY(90deg);

		width: 100%;
		height: 2px;
	}

	&__button {
		position: absolute;
		height: 100%;
		width: 50px;
		cursor: pointer;
		right: 0;
		top: 0;

		border: none;
		background-color: transparent;

		display: flex;
		align-items: center;
		justify-content: center;

		transition: transform 0.25s ease;
	}

	&__cancel-btn {
		transform: scale(0);
	}

	&__icon {
		height: 50%;
	}
}
</style>
