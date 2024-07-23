<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  }
})
</script>
<template>
  <div class="block">
    <div class="container">
      <div class="block__body">
        <div class="block__img">
          <img
            :src="`https://image.tmdb.org/t/p/w185_and_h278_bestv2/${item.poster_path}`"
            alt=""
          />
        </div>
        <div class="block__content">
          <div class="block__title">{{ item.title }}</div>
          <div class="block__desc">{{ item.overview }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.block {
  background: var(--color-grey);

  &__body {
    padding: 2rem 0;
    display: flex;
    align-items: center;
    gap: 5rem;
  }

  &__img {
    img {
      display: block;
      object-fit: cover;
      max-height: 26rem;
    }
  }

  &__title {
    font-size: 3rem;
    margin-bottom: 2rem;
  }

  &__desc {
    font-size: 1.4rem;
  }

  &._mix {
    &:nth-child(even) {
      .block {
        &__body {
          flex-direction: row-reverse;
        }
      }
    }
  }

  @media (max-width: 600px) {
    &__body {
      flex-direction: column;
      text-align: center;
    }

    &._mix {
      &:nth-child(even) {
        .block {
          &__body {
            flex-direction: column-reverse;
          }
        }
      }
    }
  }
}
</style>
