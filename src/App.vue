<template>
  <h1>ToDo App</h1>
  <form @submit.prevent="addTodo()">
    <label>New ToDo </label>
    <input v-model="newTodo" name="newTodo" autocomplete="off">
    <button>Add ToDo</button>
  </form>
  <h2>ToDo List</h2>
  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span :class="{ done: todo.done }" @click="doneTodo(todo)">{{ todo.content }}</span>
      <button @click="removeTodo(index)">Remove</button>
    </li>
  </ul>
  <h4 v-if="todos.length === 0">Empty list.</h4>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('');

const defaultData = [{
  done: false,
  content: 'Write a blog post'
}];

const todosData = JSON.parse(localStorage.getItem('todos')) || defaultData;

const todos = ref(todosData);


const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({
      done: false,
      content: newTodo.value
    });
    newTodo.value = '';
  }
  saveData();
};

const doneTodo = (todo) => {
  todo.done = !todo.done;
  saveData();
};

const removeTodo = (index) => {
  todos.value.splice(index, 1);
  saveData();
};

const saveData = () => {
  const storageData = JSON.stringify(todos.value);
  localStorage.setItem('todos', storageData);
}

</script>

<style >
body {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #27292d;
  color: white;
}

#app {

  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  padding: 20px;
}

h1 {
  font-weight: bold;
  font-size: 28px;
  text-align: center;
}

form {
  display: flex;
  flex-direction: column;
  width: 100%;
}

form label {
  font-size: 14px;
  font-weight: bold;
}

form input,
body #app form button {
  height: 48px;
  box-shadow: none;
  outline: none;
  padding-left: 12px;
  padding-right: 12px;
  border-radius: 6px;
  font-size: 18px;
  margin-top: 6px;
  margin-bottom: 12px;
}

form input {
  background-color: transparent;
  border: 2px solid rgba(255, 255, 255, 0.35);
  color: inherit;
}

button {
  cursor: pointer;
  background-color: #a0a4d9;
  border: 1px solid #a0a4d9;
  color: #1f2023;
  font-weight: bold;
  outline: none;
  border-radius: 6px;
}

h2 {
  font-size: 22px;
  border-bottom: 2px solid rgba(255, 255, 255, 0.35);
  padding-bottom: 6px;
}

ul {
  padding: 10px;
}

ul li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 2px solid rgba(255, 255, 255, 0.35);
  padding: 12px 24px;
  border-radius: 6px;
  margin-bottom: 12px;
}

ul li span {
  cursor: pointer;
}

ul li .done {
  text-decoration: line-through;
}

ul li button {
  font-size: 12px;
  padding: 6px;
}

h4 {
  text-align: center;
  opacity: 0.5;
  margin: 0;
}
</style>
