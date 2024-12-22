<script>
import { defineComponent } from 'vue'

export default defineComponent({
  setup() {
    const images = [
      {
        id: 1,
        imageUrl: 'public/i (1).webp',
      },
      {
        id: 2,
        imageUrl: 'public/i (1).webp',
      },
      {
        id: 3,
        imageUrl: 'public/i (1).webp',
      },
      {
        id: 4,
        imageUrl: 'public/i (1).webp',
      },
      {
        id: 5,
        imageUrl: 'public/i (1).webp',
      },
    ]

    return {
      images,
    }
  },
})
</script>

<template>
  <swiper-container
    class="mySwiper"
    slides-per-view="3"
    space-between="30"
    loop="true"
    navigation="true"
    pagination="true"
    autoplay-delay="2500"
    autoplay-disable-on-interaction="false"
  >
    <swiper-slide v-for="image in images" :key="image.id">
      <img :src="image.imageUrl" />
    </swiper-slide>
  </swiper-container>
</template>

<style>
.mySwiper {
  width: 800px;
  height: 400px;
  margin: 0 auto;
}

swiper-slide {
  text-align: center;
  font-size: 18px;
  background: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
}

swiper-slide img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
