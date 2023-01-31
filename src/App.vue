<script setup>
import ListItem from "./components/ListItem.vue";
</script>

<template>
	<main>
		<h1 class="green">To-do list</h1>
		<ul
			id="todoList"
			ref="todoList"
		>
			<ListItem
				v-for="(todo, index) in todos"
				:index="index"
				:description="todo.description || null"
				:done="todo.done"
				@validateInput="validateInput"
				@deleteTodo="deleteTodo"
			/>
		</ul>
		<button
			id="addTodo"
			@click="addTodo"
		>
			New todo
		</button>
	</main>
</template>
<script>
export default {
	beforeCreate() {
		document.title = "todo-list-vue";
	},
	data() {
		return {
			todos: [
				{
					description: "Finish app today",
					done: false,
				},
				{
					description: "Wash the dishes",
					done: true,
				},
				{
					description: "Prevent the Pillagers from entering the village",
					done: false,
				},
			],
		};
	},

	components: {
		ListItem,
	},

	methods: {
		addTodo() {
			this.todos.push({
				description: null,
				done: false,
			});
		},

		validateInput(value, index) {
			if (value) {
				this.todos[index].description = value;
			} else {
				this.todos.splice(index, 1);
			}
		},

		deleteTodo(index) {
			this.todos.splice(index, 1);
		},
	},
};
</script>
