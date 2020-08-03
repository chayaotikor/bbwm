<template>
  <section
    class="slide-container"
  >
  <div :style="{ backgroundImage: `url(${image})` }" class="image"> 

  </div>
    <section class="bottom-container">
    <h6 class="image-credit">{{ credit }}</h6>
      <h1 class="bottom-heading">{{ heading }}</h1>
      <div class="bottom-text"  v-html="text" v-for="(text, index) in richtext" :key="index"></div>
    </section>
  </section>
</template>
<script>
export default {
  props: {
    heading: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
    credit: {
      type: String,
      required: true,
    },
    richtext: {
      type: Array,
      required: true
    }
  },
}
</script>

<style scoped>
.slide-container {
  width: 100%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-end;
  position: relative;
  opacity: .9;
}
.image {
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  width: 100%;
  height: 60vh;

}



.bottom-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 2rem;
  color: black;
  background: white;
  width: 100%;
  position: relative;
}

.image-credit {
  color: black;
  font-size: 1rem;
  padding: 1rem;
  align-self: flex-start;
  position: absolute;
  top: 0;
  right: 0;
}
.bottom-heading {
  font-size: 2.6rem;
  font-family: 'Dosis', sans-serif;
  font-weight: bold;
  text-decoration: underline;
  padding: 1rem;
}

.bottom-text {
  font-size: 1.4rem;
  font-family: 'Lato', sans-serif;
  text-align: left;
  padding: 1rem;
}

@media only screen and (max-width: 320px) and (max-height: 320px) {
  .bottom-heading {
    font-size: 2rem;
    margin-top: 1rem;
  }
}

/* desktop Landscape */
@media only screen and (min-width: 1280px) {
  .bottom-heading {
    font-size: 3.2rem;
  }
  .bottom-text {
    font-size: 2.4rem;
  }
}
</style>
