<script setup>
import { computed } from 'vue'

const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

const value = computed({
  get() {
    return props.modelValue
  },
  set(value) {
    emit('update:modelValue', value)
  }
})

// textBox1.DataBindings.Add("Text", this, "SomeProperty", true, DataSourceUpdateMode.OnPropertyChanged);

// - the "Text" is the property of the TextBox you're binding to,
// - `this` refers to the current form (assuming the property exists on the form),
// - "SomeProperty" is the name of the property you're binding to.

// `If the user types into the TextBox, SomeProperty gets updated. If SomeProperty changes in your code, the TextBox displays the updated value.

// In both cases (Vue's v-model and WinForms' data binding), changes in the UI reflect in the data, and changes in the data reflect in the UI. This is the essence of two-way binding.
</script>

<template>
  <input v-model="value" />
</template>
