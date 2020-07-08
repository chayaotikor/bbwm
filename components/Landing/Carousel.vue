<template>
  <div class="carousel-container">
   <span class="pagination-container">
      <!-- <button 
        v-for="slide in slides"
        :key="slide.id"
        @click="setCurrentSlide(slide.id)"
        class="pagination-dot"
        :style="[
          currentSlide === 1
            ? { 'background-color': 'wheat' }
            : { 'background-color': 'white' },
        ]"
      ></button>-->
    </span>
    <!-- <section 
      class="slide-container"
      v-for="slide in slides"
      :key="slide.id"

      :style="{ backgroundImage: `url(${slide.image})` }"
    >
      <section class="bottom-container">
        <h1 class="bottom-heading">{{ slide.heading }}</h1>
        <p class="bottom-text">{{ slide.text }}</p>
      </section>
    </section> -->
  </div>
</template>

<script>
export default {
  asyncData(context) {
    console.log('sanity',context)
    return context.app.$storyapi
      .get('cdn/stories', {
        version: 'draft',
      })
      .then((res) => {
        console.log("res",res)
      })
      .catch((e) => {
        console.log(e)
      })
  },
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
  border: 1px solid red;
}

.pagination-container {
  display: flex;
  width: 100px;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  top: 1rem;
  border: 1px solid red;
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

.slide-container {
  width: 100%;
  height: 100vh;
  background-position: top;
  background-size: cover;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-end;
  opacity: 0.5;
}
.bottom-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: flex-start;
  padding: 2%;
  color: black;
  background: white;
  width: 100%;
}
.bottom-heading {
  font-size: 3.2rem;
  font-family: 'Dosis', sans-serif;
  font-weight: bold;
  text-decoration: underline;
  padding-bottom: 2.5%;
}

.bottom-text {
  font-size: 2.4rem;
  font-family: 'Lato', sans-serif;
  text-align: left;
}
</style>
