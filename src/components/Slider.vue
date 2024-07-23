<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue'
import { EffectCreative, Pagination, Navigation, Autoplay } from 'swiper/modules'
import { ref } from 'vue'

const next = ref(null)
const prev = ref(null)

const slides = ref([
  {
    text_top: 'Lorem ipsum dolor sit amet',
    text_bottom: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit',
    color: '#027d84',
    title: 'lorem ipsum',
    subtitle_1: 'Lorem ipsum dolor — ',
    subtitle_2: 'Lorem ',
    subtitle_3: 'ipsum !',
    img: '/images/dog.png'
  },
  {
    text_top: 'Lorem ipsum dolor sit amet',
    text_bottom: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit',
    color: '#4A989A',
    title: 'lorem ipsum',
    subtitle_1: 'Lorem ipsum dolor — ',
    subtitle_2: 'Lorem ',
    subtitle_3: 'ipsum !',
    img: '/images/dog.png'
  },
  {
    text_top: 'Lorem ipsum dolor sit amet',
    text_bottom: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit',
    color: '#AFB3B4',
    title: 'lorem ipsum',
    subtitle_1: 'Lorem ipsum dolor — ',
    subtitle_2: 'Lorem ',
    subtitle_3: 'ipsum !',
    img: '/images/dog.png'
  },
  {
    text_top: 'Lorem ipsum dolor sit amet',
    text_bottom: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit',
    color: '#4A989A',
    title: 'lorem ipsum',
    subtitle_1: 'Lorem ipsum dolor — ',
    subtitle_2: 'Lorem ',
    subtitle_3: 'ipsum !',
    img: '/images/dog.png'
  },
  {
    text_top: 'Lorem ipsum dolor sit amet',
    text_bottom: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit',
    color: '#AFB3B4',
    title: 'lorem ipsum',
    subtitle_1: 'Lorem ipsum dolor — ',
    subtitle_2: 'Lorem ',
    subtitle_3: 'ipsum !',
    img: '/images/dog.png'
  }
])
</script>

<template>
  <swiper
    class="slider"
    :loop="true"
    :slides-per-view="'auto'"
    :modules="[EffectCreative, Pagination, Navigation, Autoplay]"
    :autoplay="{ delay: 5000 }"
    :navigation="{
      nextEl: next,
      prevEl: prev
    }"
    effect="creative"
    :creative-effect="{
      prev: {
        translate: ['-90%', 0, 0]
      },
      next: {
        translate: ['20px', 0, 0],
        opacity: 1
      },
      limitProgress: 2
    }"
    :pagination="{
      type: 'fraction'
    }"
    :breakpoints="{
      1150: {
        creativeEffect: {
          next: {
            translate: ['40px', 0, 0],
            opacity: 1
          }
        }
      }
    }"
  >
    <swiper-slide v-for="slide of slides" class="slide" :style="{ background: slide.color }">
      <div class="slide__container">
        <img class="slide__dawn" src="/svg/dawn.svg" alt="" />
        <div class="slide__left">
          <div class="slide__text-top">{{ slide.text_top }}</div>
          <h2 class="slide__title">{{ slide.title }}</h2>
          <div class="slide__subtitle">
            <p>{{ slide.subtitle_1 }}</p>
            <p>{{ slide.subtitle_2 }}</p>
            <p>{{ slide.subtitle_3 }}</p>
          </div>

          <p class="slide__text-bottom">{{ slide.text_bottom }}</p>
        </div>
        <div class="slide__right">
          <img :src="slide.img" alt="" />
        </div>
      </div>
    </swiper-slide>
    <div class="swiper-pagination"></div>
    <div ref="next" class="swiper-button-next">
      <img src="/svg/view_next.svg" alt="view_next" class="swiper-button-text" />
      <img src="/svg/arrow_right.svg" alt="arrow_next" class="swiper-button-arrow" />
    </div>
    <div ref="prev" class="swiper-button-prev"></div>
  </swiper>
</template>

<style lang="scss">
.slide {
  position: relative;
  min-height: 70.8rem;
  color: var(--color-white);
  background: #027d84;
  border-radius: 0 9rem 9rem 0;
  flex: 0 0 100%;

  &__container {
    max-width: 118rem;
    padding: 0 2rem 0 6rem;
    margin: 0 auto;
  }

  &__text-top {
    position: relative;
    z-index: 1;
    padding: 1.8rem 0 0 3.5rem;
    font-size: 1.8rem;
    font-weight: 500;
    text-transform: uppercase;

    &::before {
      content: '';
      position: absolute;
      z-index: -1;
      top: -17rem;
      left: -7rem;
      width: 46rem;
      height: 24rem;
      background: #afb3b4;
      transform: rotate(13deg);
      border-radius: 50%;
    }
  }

  &__title {
    font-weight: 700;
    font-size: 6rem;
    line-height: 6.4rem;
    text-transform: uppercase;
    margin-top: 7rem;
    margin-bottom: 0.3rem;
  }

  &__subtitle {
    font-size: 6rem;
    line-height: 7rem;
    text-transform: uppercase;
    margin-bottom: 4.3rem;

    p {
      &:first-child {
        margin-left: 4.5rem;
      }

      &:nth-child(2) {
        margin-left: 29rem;
      }

      &:last-child {
        margin-left: 14rem;
      }
    }
  }

  &__text-bottom {
    font-weight: 500;
    font-size: 1.5rem;
    text-transform: uppercase;
    margin-left: 29rem;
    max-width: 29rem;
  }

  &__dawn {
    position: absolute;
    z-index: 5;
    bottom: 19rem;
    left: 0;
  }

  &__right {
    position: absolute;
    top: 5rem;
    right: 6%;
  }

  @media (max-width: 1400px) {
    &__right {
      right: -1rem;
    }
  }

  @media (max-width: 1250px) {
    &__text-bottom {
      margin-left: 15rem;
    }
  }

  @media (max-width: 1150px) {
    min-height: 90rem;

    &__text-top {
      margin-left: 35%;
      padding: 0.8rem 0 0 1.5rem;

      &::before {
        width: 38rem;
        height: 19.6rem;
        top: -13rem;
        left: -5rem;
      }
    }

    &__title,
    &__subtitle {
      font-size: 4rem;
      line-height: 5rem;
    }

    &__title {
      margin-left: 2.5rem;
      margin-top: 8rem;
    }

    &__subtitle {
      margin-bottom: 0rem;
      p {
        &:first-child {
          margin-left: 6.5rem;
        }

        &:nth-child(2) {
          margin-left: 26rem;
        }
      }
    }

    &__text-bottom {
      margin-left: 49%;
    }

    &__dawn {
      width: 14rem;
      height: 14rem;
      bottom: auto;
      top: 24rem;
      left: -5rem;
    }

    &__right {
      top: auto;
      right: auto;
      left: 47%;
      bottom: 3rem;
      transform: translateX(-50%);

      img {
        width: 53rem;
      }
    }
  }
}

.swiper {
  position: relative;
  width: calc(100% - 80px);

  &-pagination-fraction {
    position: absolute;
    left: 27.7rem;
    bottom: 7.2rem;
    z-index: 10;
    font-weight: 500;
    font-size: 1.6rem;
    color: var(--color-white);

    &::before {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 11.2rem;
      height: 5.8rem;
      border: 2px solid currentColor;
      border-radius: 50%;
    }
  }

  &-button-next {
    position: absolute;
    z-index: 10;
    top: 29rem;
    right: 7rem;
    cursor: pointer;
    border-radius: 50%;

    .swiper-button-text {
      animation: rotate linear 13s infinite;
    }

    .swiper-button-arrow {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }

  @media (max-width: 1150px) {
    width: calc(100% - 40px);

    &-pagination-fraction {
      left: 5.7rem;
      bottom: 4.2rem;

      &::before {
        width: 10rem;
        height: 5.2rem;
      }
    }

    &-button-next {
      top: 42rem;
      right: 2rem;
    }
  }
}

@keyframes rotate {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
