<template>
	<form @submit.prevent="formulario" class="todo-form">
		<input
			type="text"
			class="todo-form__input"
			placeholder="Create a new todo..."
			v-model.trim="text"
		/>
	</form>
</template>

<script>
import { inject, ref } from 'vue';

export default {
	setup() {
		const todos = inject('todos');
		const text = ref('');

		console.log(todos.value);

		const formulario = () => {
			if (text.value) {
				const todo = {
					text: text.value,
					status: false,
					id: Date.now(),
				};
				text.value = '';
				todos.value.push(todo);
			}
		};

		return { formulario, text };
	},
};
</script>
