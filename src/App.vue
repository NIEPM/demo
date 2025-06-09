<template>
	<div class="container">
		<h1>📝 我的待辦清單</h1>
		<input v-model="newTodo" type="text" placeholder="輸入待辦事項" />
		<button type="button" @click="addTodo">新增</button>

		<div
			v-for="(todo, index) in todos"
			:key="index"
			class="todo"
			:class="{ completed: todo.completed }"
		>
			<input type="checkbox" v-model="todo.completed" @change="saveTodos" />
			<span>{{ todo.text }}</span>
			<button type="button" @click="removeTodo(index)">刪除</button>
		</div>
	</div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue';

const newTodo = ref('');
const todos = ref([]);

const loadTodos = () => {
	const saved = localStorage.getItem('vue-todos');
	if (saved) {
		todos.value = JSON.parse(saved);
	}
};

const saveTodos = () => {
	localStorage.setItem('vue-todos', JSON.stringify(todos.value));
};

const addTodo = () => {
	const text = newTodo.value.trim();
	if (text) {
		todos.value.push({ text, completed: false });
		newTodo.value = '';
		saveTodos();
	}
};

const removeTodo = (index) => {
	todos.value.splice(index, 1);
	saveTodos();
};

onMounted(loadTodos);
watch(todos, saveTodos, { deep: true });
</script>

<style scoped>
.container {
	font-family: Arial, sans-serif;
	margin: 2em;
}

.todo {
	display: flex;
	align-items: center;
	margin-bottom: 0.5em;
}

.todo.completed span {
	text-decoration: line-through;
	color: gray;
}

.todo button {
	margin-left: 1em;
}

input[type='text'] {
	padding: 0.5em;
	width: 300px;
	margin-right: 0.5em;
}
</style>

