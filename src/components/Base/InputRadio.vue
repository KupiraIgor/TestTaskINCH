<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: {
    type: Number,
    required: true
  },
  data: {
    type: Object,
    required: true
  }
})
const emit = defineEmits(['update:modelValue', 'click'])

const localValue = computed({
  get() {
    return props.modelValue
  },
  set(e) {
    emit('update:modelValue', e)
    emit('click')
  }
})
</script>

<template>
  <label class="input-radio">
    <input
      v-model="localValue"
      type="radio"
      :checked="localValue === data.id"
      :value="data.id"
      class="input-radio__input"
    />
    <span class="input-radio__name">{{ data.name }}</span>
  </label>
</template>

<style lang="scss" scoped>
.input-radio {
  display: block;
  font-size: 1.2rem;
  text-transform: uppercase;

  &__input {
    width: 1rem;
    height: 1rem;
  }

  span {
    margin-left: 0.5rem;
  }
}
</style>
