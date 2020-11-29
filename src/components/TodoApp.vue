<template>
	<div class="todo-app">
		<span class="todo-app__title">
			TODO
		</span>
		<span class="todo-app__mode" @click="toogleMode">
			<img v-if="mode === 'sun'" src="../assets/images/icon-moon.svg" alt="" />
			<img v-if="mode === 'moon'" src="../assets/images/icon-sun.svg" alt="" />
		</span>
		<todo-form />
		<todo-list />
	</div>
</template>

<script>
import { provide, ref, watchEffect } from 'vue';
import TodoForm from './TodoForm.vue';
import TodoList from './TodoList.vue';

export default {
	name: 'TodoApp',
	components: {
		TodoForm,
		TodoList,
	},
	setup() {
		const todos = ref([]);
		provide('todos', todos);
		const mode = ref('sun');

		if (localStorage.getItem('todos')) {
			todos.value = JSON.parse(localStorage.getItem('todos'));
		}

		const toogleMode = () => {
			const body = document.querySelector('body');
			if (mode.value === 'sun') {
				body.classList.add('dark');
				mode.value = 'moon';
			} else {
				body.classList.remove('dark');
				mode.value = 'sun';
			}
		};

		watchEffect(() => {
			localStorage.setItem('todos', JSON.stringify(todos.value));
		});

		return { mode, toogleMode };
	},
};
</script>
