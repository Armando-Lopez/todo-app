<template>
	<ul class="todo-list">
		<todo-item v-for="todo in todos" :key="todo.id" :todo="todo" />
		<todo-footer v-if="todos.length" />
	</ul>
	<todo-filter />
</template>

<script>
import { computed, inject, provide, ref } from 'vue';
import TodoItem from './TodoItem.vue';
import TodoFooter from './TodoFooter.vue';
import TodoFilter from './TodoFilter.vue';

export default {
	components: { TodoItem, TodoFooter, TodoFilter },
	setup() {
		const todosTodo = inject('todos');

		const state = ref('all');

		const todos = computed(() => {
			if (state.value === 'all') {
				return todosTodo.value;
			}

			if (state.value === 'active') {
				console.log('2323');
				return todosTodo.value.filter((todo) => todo.status === false);
			}

			if (state.value === 'completed') {
				return todosTodo.value.filter((todo) => todo.status === true);
			}
		});

		provide('state', state);

		return { todos };
	},
};
</script>

<style></style>
