<script setup>
import { IMaskComponent } from 'vue-imask'

defineProps({
  modelValue: {
    type: String,
    default: ''
  },
  type: {
    type: String,
    required: false,
    default: 'text'
  },
  placeholder: {
    type: String,
    default: '',
    required: false
  },
  required: {
    type: Boolean,
    default: false
  },
  textarea: {
    type: Boolean,
    default: false
  },
  error: {
    type: Number,
    default: 0
  },
  phone: {
    type: Boolean,
    required: false,
    default: false
  }
})

const emit = defineEmits(['update:modelValue'])
</script>

<template>
  <label class="base-input" :class="{ _error: error, _textarea: textarea }">
    <span class="base-input__placeholder">{{ required ? ' * ' : '' }}{{ placeholder }}</span>
    <textarea
      v-if="textarea"
      class="base-input__input"
      :value="modelValue"
      @input="emit('update:modelValue', $event.target.value)"
    />
    <IMaskComponent
      v-else-if="phone"
      v-bind="{
        mask: '(000) 000-00-00',
        lazy: false
      }"
      :value="modelValue"
      inputmode="numeric"
      class="base-input__input"
      maxlength="17"
      @input="emit('update:modelValue', $event.target.value)"
    />
    <input
      v-else
      class="base-input__input"
      :type="type"
      :value="modelValue"
      @input="emit('update:modelValue', $event.target.value)"
    />
  </label>
</template>

<style lang="scss" scoped>
.base-input {
  display: block;

  &__placeholder {
    display: block;
    font-size: 1.2rem;
    text-transform: uppercase;
  }

  &__input {
    min-height: 3rem;
    padding: 0 1rem 0;
    border: 1px solid var(--color-black);
    width: 100%;
  }

  &._textarea {
    .base-input {
      &__input {
        min-height: 8.5rem;
        resize: none;
        display: block;
      }
    }
  }

  &._error {
    .base-input {
      &__placeholder {
        color: var(--color-red);
      }

      &__input {
        border-color: var(--color-red);
      }
    }
  }
}
</style>
