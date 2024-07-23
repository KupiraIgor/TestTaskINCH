<script setup>
import Slider from '@/components/Slider.vue'
import Form from '@/components/Form.vue'
import Blocks from '@/components/Blocks.vue'
</script>

<template>
  <div class="home">
    <Slider />
    <div class="home__forms">
      <Form />
    </div>
    <Blocks />
  </div>
</template>

<style lang="scss" scoped>
.home {
  margin-bottom: 10rem;

  &__forms {
    margin: 6rem 0 10rem;
    display: flex;
    justify-content: center;
  }
}
</style>
