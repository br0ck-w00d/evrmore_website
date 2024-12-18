<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'BasicButton',
  props: {
    variant: {
      type: String,
      default: 'default',
      validator: (value: string) => ['default', 'primary', 'secondary', 'danger'].includes(value),
    },
    size: {
      type: String,
      default: 'medium',
      validator: (value: string) => ['small', 'medium', 'large'].includes(value),
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['click'],
  setup(props, { emit }) {
    const handleClick = (event: Event) => {
      if (!props.disabled) emit('click', event);
    };
    return { handleClick };
  }
})
</script>


<template>
  <button :class="['button', variant, size]" :disabled="disabled" @click="handleClick">
    <slot></slot>
  </button>
</template>



<style scoped lang="scss">
/* Base button styles */
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: none;
  cursor: pointer;
  padding: 0.5rem 2rem;
  font-size: 1rem;
  border-radius: 32px;
  transition: background 0.2s ease;
}

/* Variants */
.default {
  background-color: #00000067;
  color: #333;
}

.primary {
  background-color: #007bff;
  color: #fff;
}

.secondary {
  background-color: #6c757d;
  color: #fff;
}

.danger {
  background-color: #dc3545;
  color: #fff;
}

/* Sizes */
.small {
  padding: 0.25rem 1rem;
  font-size: 0.875rem;
}

.medium {
  padding: 0.5rem 2rem;
  font-size: 1rem;
}

.large {
  padding: 0.75rem 2.5rem;
  font-size: 1.125rem;
}

/* Disabled state */
.button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
