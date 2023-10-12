<template>
 <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span :class="{ done: todo.done }" @click="$emit('doneTodo',todo)">{{ todo.content }}</span>

			<AppButton @buttonClicked="$emit('removeTodo', index)">Remove</AppButton>
      <!-- <button @click="removeTodo(index)">Remove</button> -->
    </li>
  </ul>
</template>

<script setup>
import AppButton from './AppButton.vue';

defineProps({
	todos: {
		type:  Array,
		required: true
	}
})

</script>

<style>
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

</style>
