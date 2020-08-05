<template>
  <div
    class="carousel-container"
    @touchstart="touchStart"
    @touchEndMethod="touchEnd"
  >
    <span class="arrow-container">
      <button
        @click="setCurrentSlide('left')"
        class="left-arrow"
        :style="{
          backgroundImage: `url(${require('../assets/images/arrow.png')})`,
        }"
      />
      <button
        @click="setCurrentSlide('right')"
        class="right-arrow"
        :style="{
          backgroundImage: `url(${require('../assets/images/arrow.png')})`,
        }"
      />
    </span>
    <Carousel
      v-for="slide in slides"
      v-editable="slide.blok"
      :key="slide.id"
      :heading="slide.heading"
      :image="slide.image"
      :text="slide.text"
      :credit="slide.credit"
      v-show="slide.index === currentSlide"
    />
  </div>
</template>

<script>
import Carousel from '@/components/Landing/Carousel'
export default {
  async asyncData(context) {
    const slideData = await context.app.$storyapi.get('cdn/stories', {
      version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      starts_with: 'carousel',
    })

    const slides = slideData.data.stories.map((slide, index) => {
      return {
        id: slide.id,
        blok: slide.content,
        index: index,
        heading: slide.content.heading,
        text: slide.content.text,
        image: slide.content.image.filename,
        credit: slide.content.credit,
      }
    })

    const currentSlide = 0
    return { slides, currentSlide }
  },
  methods: {
    setCurrentSlide(direction) {
      if (direction === 'right') {
        if (this.currentSlide === this.slides.length - 1) {
          this.currentSlide = 0
        } else {
          this.currentSlide++
        }
      }
      if (direction === 'left') {
        if (this.currentSlide === 0) {
          this.currentSlide = this.slides.length - 1
        } else {
          this.currentSlide--
        }
      }
    },
    touchStart(touchEvent) {
      if (touchEvent.changedTouches.length !== 1) {
        return
      }
      const posXStart = touchEvent.changedTouches[0].clientX
      addEventListener(
        'touchend',
        (touchEvent) => this.touchEnd(touchEvent, posXStart),
        { once: true }
      )
    },
    touchEnd(touchEvent, posXStart) {
      if (touchEvent.changedTouches.length !== 1) {
        return
      }
      const posXEnd = touchEvent.changedTouches[0].clientX
      if (posXStart < posXEnd) {
        this.setCurrentSlide('right')
      } else if (posXStart > posXEnd) {
        this.setCurrentSlide('left')
      }
    },
  },
  mounted() {
    this.$storybridge.on('change', () => {
      location.reload(true)
    })
  },
}
</script>

<style scoped>
.carousel-container {
  width: 100%;
  display: flex;
  flex-flow: column nowrap;
  margin: 0;
  position: relative;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.arrow-container {
  display: flex;
  width: 100%;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  top: 50vh;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9;
}

.left-arrow {
  border-radius: 50%;
  transform: rotate(180deg);
  height: 48px;
  width: 48px;
  margin: 2.5%;
  cursor: pointer;
  border: none;
}
.right-arrow {
  border-radius: 50%;
  height: 48px;
  width: 48px;
  margin: 2.5%;
  cursor: pointer;
  border: none;
}
</style>
