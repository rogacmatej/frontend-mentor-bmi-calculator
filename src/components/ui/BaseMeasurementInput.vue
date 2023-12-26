<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  inputId: string
  name: string
  unit: string
  modelValue?: number
  placeholder?: string
  readonly?: boolean
  disabled?: boolean
  ariaLabel?: string
  ariaLabeledBy?: string
}

const props = withDefaults(defineProps<Props>(), {
  placeholder: '0',
  disabled: false,
  readonly: false
})
const emit = defineEmits(['update:modelValue'])

const value = computed({
  get() {
    return props.modelValue
  },
  set(value) {
    if (!props.disabled) {
      emit('update:modelValue', parseFloat('' + value) || undefined)
    }
  }
})
</script>

<template>
  <div class="measurement-input">
    <input
      type="number"
      :id="props.inputId"
      :name="props.name"
      :placeholder="props.placeholder"
      :disabled="props.disabled"
      v-model.number="value"
    />
    <span class="unit">{{ unit }}</span>
  </div>
</template>

<style scoped>
.measurement-input {
  position: relative;
}

.unit {
  position: absolute;
  color: #345ff6;
  font-size: 2.4rem;
  font-style: normal;
  font-weight: 600;
  line-height: normal;
  letter-spacing: -0.12rem;
  right: 2.4rem;
  top: 50%;
  transform: translateY(-50%);
}

input {
  padding: 2rem 8rem 2rem 2.4rem;
  appearance: none;
  font-size: 2.4rem;
  font-style: normal;
  font-weight: 600;
  line-height: normal;
  letter-spacing: -0.12rem;
  border: 1px solid #d8e2e7;
  border-radius: 1.2rem;
  width: 100%;
}

input:not(:disabled):hover,
input:not(:disabled):focus-visible {
  outline: 0;
  border-color: hsl(227, 92%, 58%, 1);
}

input::placeholder {
  opacity: 0.25;
}

input:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>
