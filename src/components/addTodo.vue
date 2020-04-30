<template>
	<form @submit.prevent="onSubmit">
		<input type="text" v-model="title">
		<button type="submit">Create</button>
	</form>
</template>

<script>
	export default {
		name: "addTodo",
		data() {
			return {
				title: ''
			}
		},
		methods: {
			onSubmit() {
				if (this.title.trim()) {
					let item = {
						id: Date.now(),
						title: this.title,
						complited: false
					};
					this.$emit("add-todo", item);
					this.title = '';
				}

			}
		}
	}
</script>

<style scoped>
	form {
		display: inline-flex;
		padding: 10px;
	}

	infinity {
		width: 400px;
	}

</style>