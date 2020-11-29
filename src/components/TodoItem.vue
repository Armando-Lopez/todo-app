<template>
	<li class="todo-list__item">
    <span class="todo-list__item__status" :class="{ 'completed': todo.status }" >
      <img v-if="todo.status" src="../assets/images/icon-check.svg" alt="">
    </span>
		<span
      role="button"
      @click="toggleComplete(todo.id)"
      class="todo-list__item__text"
      :class="{ 'completed': todo.status }"
    >
			{{ todo.text }}
		</span>
		<span class="todo-list__item__cross" @click="deleteTodo(todo.id)">
      <img src="../assets/images/icon-cross.svg" alt="">
		</span>
	</li>
</template>

<script>
import { inject } from 'vue';

export default {
	name: 'TodoItem',
	props: {
		todo: {
			type: Object,
			default: () => {},
			required: true,
		},
	},
	setup() {
		const todos = inject('todos');

		const deleteTodo = (id) => {
			todos.value = todos.value.filter((item) => item.id !== id);
		};

		const toggleComplete = (id) => {
			todos.value = todos.value.map((item) => {
				if (item.id === id) {
					item.status = true;
				}
				return item;
			});
		};
		return { deleteTodo, toggleComplete };
	},
};
</script>

<style>
.completed {
	text-decoration: line-through;
}
</style>
