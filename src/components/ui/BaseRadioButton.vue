<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  modelValue: string
  value: string
  inputId: string
  name: string
  disabled?: boolean
  ariaLabel?: string
  ariaLabeledBy?: string
}
const props = withDefaults(defineProps<Props>(), {
  disabled: false
})
const emit = defineEmits(['update:modelValue'])

const onChange = (e: Event) => {
  emit('update:modelValue', (e.target as HTMLInputElement).value)
}

const isChecked = computed(() => {
  return props.modelValue === props.value
})
</script>

<template>
  <input
    type="radio"
    :id="props.inputId"
    :name="props.name"
    :disabled="props.disabled"
    :aria-label="props.ariaLabel"
    :ariaLabeledBy="props.ariaLabeledBy"
    :value="props.value"
    :checked="isChecked"
    @change="onChange"
  />
</template>

<style scoped>
input[type='radio'] {
  width: 3.1rem;
  height: 3.1rem;
  appearance: none;
  border: 1px solid #d8e2e7;
  border-radius: 50%;
  display: grid;
  place-content: center;
  transition: all 0.3s ease-in-out;
}

input[type='radio']:not(:disabled):hover,
input[type='radio']:not(:disabled):focus-visible {
  border-color: hsl(227, 92%, 58%, 1);
}

input[type='radio']:not(:disabled):checked {
  border-color: hsla(227, 92%, 58%, 0.15);
  background-color: hsla(227, 92%, 58%, 0.15);
}

input[type='radio']:not(:disabled):checked::after {
  content: ' ';
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  background: hsl(227, 92%, 58%, 1);
}

input[type='radio']:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
