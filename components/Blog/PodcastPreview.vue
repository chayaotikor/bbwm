<template>
  <div class="post-container">
    <div class="line-point">
      <i class="left-arrow" />
      <span class="line">
        <!-- <h2 class="date">{{ date }}</h2> -->
      </span>
      <span class="dot" />
    </div>
    <button class="podcast-container">
      <div
        class="podcast-thumbnail"
        :style="{
          backgroundImage: `url(${require('../../assets/images/podcast.jpg')})`,
        }"
      >
        <h1 class="podcast-title">{{ title }}</h1>
      </div>
      <div class="bottom-container">
        <span
          class="play-button"
          :style="{
            backgroundImage: `url(${require('../../assets/images/playbutton.svg')})`,
          }"
        />
        <span class="play-line" />
      </div>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    date: {
      type: String,
      required: true
    }

  },
}
</script>

<style scoped>
.post-container {
  width: 100%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-between;
  align-items: space-between;
  position: relative;
}

.line-point {
  width: 100%;
  height: 16px;
  display: flex;
  align-self: flex-end;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: flex-end;
  position: absolute;
  top: -8px;
  right: -8px;
}
.line {
  border: 1px solid white;
  color: white;
  background-color: white;
  width: 100%;
  height: 2px;
  display: flex;
  z-index: 5;
  justify-content: center;
}

.date {
  position: absolute;
  top: -10px;
  font-size: 16px;
}

.left-arrow {
  border: solid white;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
}

.dot {
  height: 16px;
  width: 16px;
  border-radius: 50%;
  border: 1px solid white;
  background: white;
  margin: 0;
  z-index: 1;
}
.podcast-container {
  text-decoration: none;
  width: 70%;
  height: 25vh;
  border: 1px solid white;
  display: flex;
  margin: 2.5% 5% 5%;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  cursor: pointer;
  align-self: flex-start;
  padding: 0;
}

.podcast-thumbnail {
  background-position: center;
  background-size: cover;
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  height: 70%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
}

.podcast-title {
  font-size: 2rem;
  color: white;
  margin: 0 2rem;
}

.bottom-container {
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: space-around;
  padding: 0 2.5%;
  width: 100%;
  height: 30%;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  background: black;
}
.play-button{
  background-color: none;
  height: 24px;
  width: 24px;
  background-position: center;
  background-size: cover;
}

.play-line {
height: 2px;
width: 80%;
background-color: white;
  
}

</style>
