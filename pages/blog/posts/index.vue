<template>
  <div class="main-container">
    <section class="headings-container">
      <h1 class="column-label">Speaking Engagements</h1>
      <h1 class="column-label">Blog Posts</h1>
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

<style scoped>
.main-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
  margin-top: 6rem;
}

.timeline-container {
  display: flex;
  padding-top: 1rem;
  min-height: 100vh;
  flex-flow: row nowrap;
  justify-content: space-evenly;
  align-items: flex-start;
  padding-bottom: 0;
  position: relative;
  overflow-y: hidden;
}

.headings-container {
  top: 0;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.column-label {
  color: white;
  font-size: 1.6rem;
  font-weight: bold;
  width: 50%;
  margin: 0 2.5%;
  text-align: center;
}

.middle-line {
  position: absolute;
  min-height: 100%;
  width: 3px;
  background-color: white;
}

.left-container {
  width: 50%;
  min-height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

.right-container {
  width: 50%;
  min-height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

@media only screen and (max-width: 320px) {
  .column-label {
    font-size: 1.4rem;
  }
}

/* Tablet Portrait */
@media only screen and (min-width: 768px) {
  .column-label {
    font-size: 2.4rem;
  }
}

/* Large Tablet Landscape*/
@media only screen and (orientation: Landscape) and (min-width: 1280px) {
  .column-label {
    width: 35%;
  }
}
</style>
