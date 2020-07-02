<template>
  <div class="carousel-container">
    <span class="pagination-container">
      <button @click="setCurrentSlide(1)" class="pagination-dot" :style="[currentSlide === 1 ? {'background-color': 'wheat'} : {'background-color': 'white'}]"></button>
      <button @click="setCurrentSlide(2)" class="pagination-dot" :style="[currentSlide === 2 ? {'background-color': 'wheat'} : {'background-color': 'white'}]"></button>
      <button @click="setCurrentSlide(3)" class="pagination-dot" :style="[currentSlide === 3 ? {'background-color': 'wheat'} : {'background-color': 'white'}]"></button>
    </span>
    <section
      class="slide-container"
      v-for="slide in slides"
      :key="slide.id"
      v-show="slide.id === currentSlide"
      :style="{backgroundImage: `url(${slide.image})`}"
    >
      <section class="bottom-container">
        <h1 class="bottom-heading">{{slide.heading}}</h1>
        <p class="bottom-text">{{slide.text}}</p>
      </section>
    </section>
  </div>
</template>


<script>
 //v-show="slide.id === currentSlide"
import background1 from '@/assets/images/background1.jpg'
import background2 from '@/assets/images/background2.jpg'
import background3 from '@/assets/images/background3.jpg'

export default {
   data() {
       return {
        currentSlide: 1,
           slides: [
              { 
               id: 1,
               image: background1,
               heading: 'Visualize',
               text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'},
              { 
               id: 2,
               image: background2,
               heading: 'Plan',
               text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'},
              { 
               id: 3,
               image: background3,
               heading: 'Execute',
               text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.'},
           ]
       } 
   },
   methods: {
        setCurrentSlide(id){
            console.log(this.currentSlide)
           this.currentSlide = id
            console.log(this.currentSlide)

           
       }
   }
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



.slide-container {
  width: 100%;
  height: 100vh;
  background-position: top;
  background-size: cover;
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-end;
    opacity: .5;

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