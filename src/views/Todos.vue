<template>
	<div>
		<router-link to="/">Home</router-link>
		<hr>
		<add-todo @add-todo="addsTodo"></add-todo>
		<select v-model="filter">
			<option value="all">All</option>
			<option value="completed">Completed</option>
			<option value="not-completed">Not Completed</option>
		</select>
		<hr>
		<loader v-if="loading"/>
		<TodoList
				v-else-if="filteredTodo.length"
				v-bind:todos="filteredTodo"
				@remove-todo="removeTodo"
		></TodoList>
		<p v-else> No toods!</p>
	</div>
</template>

<script>
	import TodoList from '@/components/TodoList'
	import addTodo from "@/components/addTodo";
	import Loader from "@/components/Loader";

	export default {
		name: 'App',
		data() {
			return {
				todos: [],
				loading: true,
				filter: 'all'
			}
		},
		mounted() {
			fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
				.then(response => response.json())
				.then(json => {
					setTimeout(() => {
						this.todos = json;
						this.loading = false;
					}, 5000)
				})
		},
		components: {
			TodoList,
			addTodo,
			Loader
		},
		// watch: {
		// 	filter(val) {
		// 		console.log(val);
		// 	}
		// },
		computed: {
			filteredTodo() {
				switch (this.filter) {
					case "all":
						return this.todos;
					case "completed":
						return this.todos.filter(t => t.completed);
					case "not-completed":
						return this.todos.filter(t => !t.completed);
					default:
						return this.todos;
				}
			}
		},
		methods: {
			removeTodo(id) {
				this.todos = this.todos.filter(t => t.id !== id);
			},
			addsTodo(todo) {
				this.todos.push(todo);
			}
		}
	}
</script>
<style scoped>

</style>