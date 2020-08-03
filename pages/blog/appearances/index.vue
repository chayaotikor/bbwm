<template>
<div class="main-container">
  <div class="post-container" v-for="appearance in appearances" :key="appearance.id" v-editable="appearance.blok" >
    <div class="line-point">
      <i class="right-arrow" />
      <span class="line">
        <!-- <h2 class="date">{{ date }}</h2> -->
      </span>
      <span class="dot" />
    </div>
    <button class="appearance-container" @click="currentVid(appearance.link)" >
      <div
        class="appearance-thumbnail"
        :style="{
          backgroundImage: `url(${require('../../../assets/images/podcast.jpg')})`,
        }"
      >
        <h1 class="appearance-title">{{ appearance.title }}</h1>
      </div>
      <div class="bottom-container">
        <span
          class="play-button"
          :style="{
            backgroundImage: `url(${require('../../../assets/images/playbutton.svg')})`,
          }"
        />
        <span class="play-line" />
      </div>
    </button>
  </div>
</div>
</template>

<script>
import moment from 'moment'

export default {
  async asyncData(context) {

    const appearanceData = await context.app.$storyapi.get('cdn/stories', {
      version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      starts_with: 'blog/appearances',
    })
    
    const appearances = appearanceData.data.stories.map((appearance) => {
      return {
        id: appearance.id,
        blok: appearance.content,
        title: appearance.content.title,
        link: appearance.content.link,
        date: moment(appearance.created_at).format('MMMM DD[,] YYYY'),
      }
    })
    return { appearances }
  },
  methods: {
    currentVid(link) {
      window.open(link, '_blank')
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
.main-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
  margin-top: 8rem;
  border-left: 2px solid white;
  width: 90vw;
  height: 100%;
}
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
  flex-flow: row-reverse nowrap;
  align-items: center;
  justify-content: flex-end;
  position: absolute;
  top: -8px;
  left: -7px;
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

.right-arrow {
  border: solid white;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
}
.dot {
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 1px solid white;
  background: white;
  margin: 0;
  z-index: 1;
}
.appearance-container {
  text-decoration: none;
  width: 90%;
  height: 25vh;
  border: 1px solid white;
  display: flex;
  margin: 5%;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  cursor: pointer;
  align-self: flex-start;
  padding: 0;
}

.appearance-thumbnail {
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

.appearance-title {
  font-size: 1.6rem;
  color: white;
  font-weight: bold;
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
.play-button {
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

@media only screen and (orientation: Landscape) {
  .appearance-container {
    height: 40vh;
  }
  
}

@media only screen and (max-width: 320px) and (max-height: 320px) {
  .appearance-title {
    font-size: 0.8rem;
  }
  .play-button {
    height: 16px;
    width: 16px;
  }
}

/* Tablet Portrait */
@media only screen and (orientation: Portrait) and (min-width: 768px) {
  .appearance-title {
    font-size: 2.2rem;
  }
}

/* Tablet Landscape */
@media only screen and (orientation: Landscape) and (min-width: 1024px) {
  .appearance-title {
    font-size: 2.4rem;
  }
}

/* Large Tablet Portrait*/
@media only screen and (orientation: Portrait) and (min-width: 1024px) {
  .appearance-title {
    font-size: 2.4rem;
  }
}

/* Large Tablet Landscape*/
@media only screen and (orientation: Landscape) and (min-width: 1280px) {
  .appearance-container {
    width: 70%;
  }
  .appearance-title {
    font-size: 2.8rem;
  }
}
</style>
