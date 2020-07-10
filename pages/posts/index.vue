<template>
  <div class="timeline-container">
    <section class="left-container">
      <PodcastPreview
        v-for="podcast in podcasts"
        v-editable="podcast.blok"
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
        v-editable="post.blok"
        :key="post.id"
        :title="post.title"
        :excerpt="post.excerpt"
        :image="post.image"
        :date="post.date"
        :id="post.id"
      />
    </section>
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
      version: 'draft',
      starts_with: 'blog/posts',
    })
    const podcastData = await context.app.$storyapi.get('cdn/stories', {
      version: 'draft',
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
        id: post.id,
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
        window.open(link, "_blank")
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
.timeline-container {
  display: flex;
  padding-top: 2rem;
  flex-flow: row nowrap;
  justify-content: space-evenly;
  align-items: flex-start;
  position: relative;
  overflow-y: clip;
}
.middle-line {
  position: absolute;
  min-height: 100%;
  width: 3px;
  background-color: white;
}

.video-modal {
  position: absolute;
  z-index: 100;
  border: 1px solid red;
  top: 50%;
  width: 640px;
  height: 264px;
  color:red;
  background-color: white;
}

.left-container {
  width: 50%;
  height: 100vh;
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
</style>
