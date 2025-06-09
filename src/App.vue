<template>
	<div class="container">
		<h1>📝 我的待辦清單</h1>
		<input v-model="newTodo" type="text" placeholder="輸入待辦事項" />
		<button type="button">新增</button>

		<div v-for="(todo, index) in todos" :key="index" class="todo">
			<input type="checkbox" />
			<span>{{ todo.text }}</span>
			<button type="button">刪除</button>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('');
const todos = ref([]);
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

