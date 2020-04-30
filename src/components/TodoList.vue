<template>
	<div>
		<ul>
			<todo-item
					v-for="(item, i) in todos"
					v-bind:key="item.id"
					v-bind:index="i"
					v-bind:item="item"
					v-on:remove-todo="removeTodo"
			></todo-item>
		</ul>
	</div>
</template>

<script>
	import TodoItem from "@/components/TodoItem";

	export default {
		name: "todo list",
		props: ['todos'],
		components: {
			TodoItem
		},
		methods: {
			removeTodo(id) {
				this.$emit('remove-todo', id);
			}
		}
	}
</script>

<style scoped>

	ul {
		list-style: none;
		margin: 0;
		padding: 0;
	}

</style>