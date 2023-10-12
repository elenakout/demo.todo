<template>
<label><slot></slot></label>
    <input v-model="data" name="newTodo" autocomplete="off">
</template>

<script setup>
import { useVModel } from '@vueuse/core';

const props = defineProps({
	modelValue: {
		type: String,
		required:true
	},
})

const emit = defineEmits(['update:modelValue']);

const data = useVModel(props, 'modelValue', emit);
</script>

<style>

label {
  font-size: 14px;
  font-weight: bold;
}

input {
  height: 48px;
  box-shadow: none;
  outline: none;
  padding-left: 12px;
  padding-right: 12px;
  border-radius: 6px;
  font-size: 18px;
  margin-top: 6px;
  margin-bottom: 12px;
  background-color: transparent;
  border: 2px solid rgba(255, 255, 255, 0.35);
  color: inherit;
}

</style>
