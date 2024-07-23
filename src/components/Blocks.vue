<script setup>
import { ref } from 'vue'
import InputRadio from '@/components/Base/InputRadio.vue'
import Block from '@/components/Base/Block.vue'

const radioButtons = [
  { id: 1, name: 'відсортувати блоки за заголовком відповідно до алфавітного порядку' },
  { id: 2, name: 'Вивести всі блоки у форматі "зображення - зліва, текст - справа"' },
  {
    id: 3,
    name: 'вивести всі блоки у форматі "зображення - зліва, текст - справа" і навпаки в шаховому порядку'
  }
]
const radio = ref(1)
const isMixBlocks = ref(false)
const items = ref(null)
const sortItems = ref(null)

const onFetch = async () => {
  await fetch(
    'https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1'
  )
    .then((response) => response.json())
    .then((data) => (items.value = data.results.slice(0, 5)))
  sortItems.value = items.value.slice(0)
  onSort()
}

onFetch()
const onSort = () => {
  isMixBlocks.value = false
  if (radio.value === 1) {
    sortItems.value.sort((a, b) => a.title.toLowerCase().localeCompare(b.title.toLowerCase()))
  } else if (radio.value === 2) {
    sortItems.value = items.value.slice(0)
  } else {
    sortItems.value = items.value.slice(0)
    isMixBlocks.value = true
  }
}
</script>

<template>
  <div class="blocks">
    <div class="container">
      <div class="blocks__body">
        <div class="blocks__radios">
          <InputRadio
            class="blocks__radio"
            v-model="radio"
            v-for="item of radioButtons"
            :data="item"
            @click="onSort"
          />
        </div>
        <div v-if="sortItems" class="blocks__items">
          <Block v-for="item of sortItems" :item="item" :class="{ _mix: radio === 3 }" />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.blocks {
  &__radio {
    margin-bottom: 2rem;
  }

  &__radios {
    margin: 0 auto 5rem;
    max-width: max-content;
  }

  &__items {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }
}
</style>
