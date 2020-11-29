<template>
	<div class="todo-filter">
		<div class="todo-filter__options">
			<span class="todo-filter__option" @click="addFilter('active')">
				Activos
			</span>
			<span class="todo-filter__option" @click="addFilter('all')">
				todos
			</span>
			<span class="todo-filter__option" @click="addFilter('completed')">
        Completados
      </span>
		</div>
	</div>
</template>

<script>
import { inject } from 'vue';

export default {
	setup() {
		const state = inject('state');

		const addFilter = (val) => {
      state.value = val;
		  console.log(state);
		};

		return { addFilter };
	},
};
</script>

<style></style>
