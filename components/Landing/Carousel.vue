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
    text: {
      type: Object,
      required: true
    }
  },
    computed: {
    richtext() {
     const textArr = this.text.content.map(text => {
      return text
        ? this.$storyapi.richTextResolver.renderNode(text)
        : ''
      })
      return textArr

    },
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
  align-items: center;
  padding: 1rem;
  color: white;
  background: black;
  width: 100%;
  min-height: 31vh;
  position: relative;
  border-top: 1px solid white;
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
  text-align: center;
  width: 70%;
  text-decoration: underline;
  padding: 1rem;
}

.bottom-text {
  font-size: 1.4rem;
  font-family: 'Lato', sans-serif;
  text-align: center;
  padding: 1rem;
  width: 70%;
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
