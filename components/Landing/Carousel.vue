<template>
  <section
    class="slide-container"
    :style="{ backgroundImage: `url(${image})` }"
  >
  <h6>{{credit}}</h6>
    <section class="bottom-container">
      <h1 class="bottom-heading">{{ heading }}</h1>
      <p class="bottom-text">{{ text }}</p>
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
    text: {
      type: String,
      required: true,
    },
    credit: {
      type: String,
      required: true,
    }
  },
}
</script>

<style scoped>
.slide-container {
  width: 100%;
  height: 100vh;
  background-position: top;
  background-size:cover;
  background-repeat: no-repeat;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-end;
  opacity: 0.8;
}
.bottom-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: flex-start;
    padding: 2rem;

  color: black;
  background: white;
  width: 100%;
  height:100px;
}
.bottom-heading {
  font-size: 2.6rem;
  font-family: 'Dosis', sans-serif;
  font-weight: bold;
  text-decoration: underline;
  padding-bottom: 1rem;
}

.bottom-text {
  font-size: 1.4rem;
  font-family: 'Lato', sans-serif;
  text-align: left;
}

@media only screen and (max-width: 320px) and (max-height: 320px){
  .bottom-heading{
    font-size: 2rem;
    margin-top: 1rem;
  }
}

/* desktop Landscape */
@media only screen and (min-width: 1280px) {
.bottom-heading{
font-size: 3.2rem;
}
.bottom-text{
  font-size: 2.4rem;
}
}
</style>
