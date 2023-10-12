<template>
  <label><slot></slot></label>
  <input :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" name="newTodo" autocomplete="off">
</template>

<script setup>
defineProps({
  modelValue: {
    type: String,
    required: true
  }
});

defineEmits(['update:modelValue']);

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
