# PAGES

This directory contains your Application Views and Routes.
The framework reads all the `*.vue` files inside this directory and creates the router of your application.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/guide/routing).



<template>
  <div class="post-container" v-editable="blok">
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
      required: true,
    },
    blok: {
      type: Object,
      required: true,
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
  right: -6px;
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
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 1px solid white;
  background: white;
  margin: 0;
  z-index: 1;
}
.podcast-container {
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

@media only screen and (max-width: 320px) and (max-height: 320px) {
  .podcast-title {
    font-size: 0.8rem;
  }
  .play-button {
    height: 16px;
    width: 16px;
  }
}

/* Tablet Portrait */
@media only screen and (orientation: Portrait) and (min-width: 768px) {
  .podcast-title {
    font-size: 2.2rem;
  }
}

/* Tablet Landscape */
@media only screen and (orientation: Landscape) and (min-width: 1024px) {
  .podcast-title {
    font-size: 2.4rem;
  }
}

/* Large Tablet Portrait*/
@media only screen and (orientation: Portrait) and (min-width: 1024px) {
  .podcast-title {
    font-size: 2.4rem;
  }
}

/* Large Tablet Landscape*/
@media only screen and (orientation: Landscape) and (min-width: 1280px) {
  .podcast-container {
    width: 70%;
  }
  .podcast-title {
    font-size: 2.8rem;
  }
}
</style>





<template>
  <div class="main-container">
    <section class="headings-container">
    </section>
    <div class="timeline-container">
      <section class="left-container">
        <PodcastPreview
          v-for="podcast in podcasts"
          :blok="podcast.blok"
          :key="podcast.id"
          :title="podcast.title"
          :date="podcast.date"
          :id="podcast.id"
          :link="podcast.link"
          @click.native="currentVid(podcast.link)"
        />
      </section>
      <span class="middle-line" />
      <section class="right-container">
        <ArticlePreview
          v-for="post in posts"
          :blok="post.blok"
          :key="post.id"
          :title="post.title"
          :excerpt="post.excerpt"
          :image="post.image"
          :date="post.date"
          :id="post.id"
        />
      </section>
    </div>
  </div>
</template>

<script>
import ArticlePreview from '@/components/Blog/ArticlePreview'
import PodcastPreview from '@/components/Blog/PodcastPreview'
import moment from 'moment'

export default {
  components: {
    ArticlePreview,
    PodcastPreview,
  },
  async asyncData(context) {
    const postData = await context.app.$storyapi.get('cdn/stories', {
      version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      starts_with: 'blog/posts',
    })
    const podcastData = await context.app.$storyapi.get('cdn/stories', {
      version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      starts_with: 'blog/podcasts',
    })
    
    const podcasts = podcastData.data.stories.map((podcast) => {
      return {
        id: podcast.id,
        blok: podcast.content,
        title: podcast.content.title,
        link: podcast.content.link,
        date: moment(podcast.created_at).format('MMMM DD[,] YYYY'),
      }
    })
    const posts = postData.data.stories.map((post) => {
      return {
        id: post.slug,
        blok: post.content,
        title: post.content.title,
        excerpt: post.content.excerpt,
        image: post.content.image.filename,
        date: moment(post.created_at).format('MMMM DD[,] YYYY'),
      }
    })
    return { posts, podcasts }
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


