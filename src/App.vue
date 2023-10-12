<template>
  <h1>ToDo App</h1>
  <form>
    <AppInput v-model="newTodo">New ToDo</AppInput>

    <AppButton @buttonClicked="addTodo()">Add ToDo</AppButton>

  </form>
  <h2>ToDo List</h2>
  <AppList @doneTodo="doneTodo" @removeTodo="removeTodo" :todos="todos"/>
  <!-- <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span :class="{ done: todo.done }" @click="doneTodo(todo)">{{ todo.content }}</span>
      <button @click="removeTodo(index)">Remove</button>
    </li>
  </ul> -->
  <h4 v-if="todos.length === 0">Empty list.</h4>
</template>

<script setup>
import { ref } from 'vue';
import AppInput from './components/AppInput.vue';
import AppButton from './components/AppButton.vue'
import AppList from './components/AppList.vue';


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

h2 {
  font-size: 22px;
  border-bottom: 2px solid rgba(255, 255, 255, 0.35);
  padding-bottom: 6px;
}


h4 {
  text-align: center;
  opacity: 0.5;
  margin: 0;
}
</style>
