<template>
	<li class="todo-footer">
		<span role="button"> {{ countActives }} Activos </span>
		<span class="todo-footer__delete" @click="deleteCompleted">
			Eliminar Completados
		</span>
	</li>
</template>

<script>
import { computed, inject } from 'vue';
export default {
	setup() {
		const todos = inject('todos');

		const countActives = computed(() => {
			return todos.value.filter((todo) => todo.status === false).length;
		});

		const deleteCompleted = () => {
			todos.value = todos.value.filter((todo) => todo.status === false);
		};

		return { countActives, deleteCompleted };
	},
};
</script>

<style></style>
