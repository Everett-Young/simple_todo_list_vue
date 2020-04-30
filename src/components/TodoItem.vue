<template>
	<li v-bind:class="{done : item.completed}">
		<span class="todo-title">
			<input
					type="checkbox"
					v-on:change="item.completed=!item.completed">
			<strong>{{index + 1}}</strong>
			{{item.title | uppercase}}
		</span>
		<button class="rm"
				v-on:click="$emit('remove-todo', item.id)"
		>&times;
		</button>
	</li>
</template>

<script>
	export default {
		name: "TodoItem",
		props: {
			item: {
				type: Object,
				required: true
			},
			index: Number
		},
		filters: {
			uppercase(value) {
				return value.toUpperCase();
			}
		}
	}
</script>

<style scoped>

	li {
		border: 1px solid #cccccc;
		display: flex;
		justify-content: space-between;
		padding: 0.5rem 2rem;
		margin-bottom: 1rem;
		align-items: center;
	}

	.rm {
		background: red;
		color: #fff;
		border-radius: 50%;
		border: none;
		font-weight: bold;
		outline: red;
	}

	.done {
		background-color: #99fec5;
	}

	.done .todo-title {
		text-decoration: line-through;
	}

	input {
		margin-right: 1rem;
	}

</style>