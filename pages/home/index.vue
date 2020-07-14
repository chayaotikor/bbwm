<template>
  <div class="carousel-container">
    <span class="pagination-container">
      <button
        v-for="slide in slides"
        :key="slide.index"
        @click="setCurrentSlide(slide.index)"
        class="pagination-dot"
        :style="[
          currentSlide === slide.index
            ? { 'background-color': 'wheat' }
            : { 'background-color': 'white' },
        ]"
      ></button>
    </span>
    <Carousel
      v-for="slide in slides"
      v-editable="slide.blok"
      :key="slide.id"
      :heading="slide.heading"
      :image="slide.image"
      :text="slide.text"
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
      starts_with: 'carousel/slides',
    })

    const slides = slideData.data.stories.map((slide, index) => {
      return {
        id: slide.id,
        blok: slide.content,
        index: index,
        heading: slide.content.heading,
        text: slide.content.text,
        image: slide.content.image.filename,
      }
    })

    const currentSlide = 0
    return { slides, currentSlide }
  },
  methods: {
    setCurrentSlide(id) {
      this.currentSlide = id
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
  height:99.8vh;
  position: relative;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.pagination-container {
  display: flex;
  width: 100px;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  top: 8rem;
  z-index: 9;
}

.pagination-dot {
  border-radius: 50%;
  height: 16px;
  width: 16px;
  margin: 2.5%;
  cursor: pointer;
  border: none;
}

</style>
