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

		<img
			@mousedown="clearInput"
			class="search__icon search__icon-cancel"
			src="../assets/cancel-icon.svg"
			alt=""
		/>
		<img
			@click="focus"
			class="search__icon search__icon-search"
			src="../assets/search-icon.svg"
			alt=""
		/>
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
		padding: 12px 20px;
		width: 100%;

		color: #333;
		font-family: 'Montserrat', 'Arial', sans-serif;
		font-weight: 300;
		font-size: inherit;

		border: none;
		outline: none;

		&:focus + .search__border {
			transform: rotateX(0deg);
			background-color: #4169e1;
		}

		&:focus ~ .search__icon-cancel {
			transform: scale(1);
		}

		&:focus ~ .search__icon-search {
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

	&__icon {
		position: absolute;
		height: 100%;
		right: 0;
		top: 0;
		padding: 15px;
		cursor: pointer;

		transition: transform 0.25s ease;
	}

	&__icon-cancel {
		transform: scale(0);
	}
}
</style>
