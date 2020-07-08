<template>
      <div class="carousel-container">
       <span class="pagination-container">
      <button
        v-for="slide in slides"
        :key="slide.id"
        @click="setCurrentSlide(slide.id)"
        class="pagination-dot"
        :style="[
          currentSlide === slide.id
            ? { 'background-color': 'wheat' }
            : { 'background-color': 'white' },
        ]"
      ></button>
    </span>
    <Carousel 
        v-for="slide in slides"
        :key="slide.id"
        :heading="slide.heading"
        :image="slide.image"
        :text="slide.text"
        v-show="slide.id === currentSlide"
    />
    </div>
</template>

<script>
import Carousel from '@/components/Landing/Carousel'
export default {
    async asyncData(context){
    const slideData = await context.app.$storyapi.get(
      'cdn/stories',
      {version: 'draft',
        starts_with:'carousel/slides'
    })

    const slides = slideData.data.stories.map(slide => {
          return {
            id: slide.id,
            heading: slide.content.heading,
            text:slide.content.text,
            image: slide.content.image.filename,
          };
    })

    const currentSlide = 1
    return {slides, currentSlide}
  },
  //  methods: {
  //       setCurrentSlide(id){
  //           console.log(currentSlide)
  //          currentSlide = id
  //           console.log(currentSlide)
  //      }
  //  }
}
</script>


<style scoped>
.carousel-container {
  width: 100%;
  display: flex;
  flex-flow: column nowrap;
  margin: 0 auto;
  display: flex;
  position: relative;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-top: 6rem;
  height: calc(100vh - 6rem);
}

.pagination-container {
  display: flex;
  width: 100px;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  top: 1rem;
}

.pagination-dot {
  border-radius: 50%;
  height: 16px;
  width: 16px;
  margin: 2.5%;
  cursor: pointer;
  z-index: 50;
  border: none;
}



</style>
