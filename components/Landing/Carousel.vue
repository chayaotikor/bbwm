<template>

    <section
      class="slide-container"
      :style="{ backgroundImage: `url(${image})` }"
    >
      <section class="bottom-container">
        <h1 class="bottom-heading">{{heading }}</h1>
        <p class="bottom-text">{{text }}</p>
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
      required: true
    },
    text: {
      type:String,
      required:true
      }
  },
}
</script>

<style scoped>

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
