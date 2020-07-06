<template>
  <div class="timeline-container">
    <section class="left-container">
      <PodcastPreview  v-for="post in posts" :key="post.id" :title="post.title"
          :excerpt="post.excerpt"
          :thumbnailUrl="post.thumbnailUrl"
          :date="post.date"
          :id="post.id"/>
    </section>
    <span class="middle-line" />
    <section class="right-container">
      <ArticlePreview
        v-for="post in posts"
        :key="post.id"
        :title="post.title"
        :excerpt="post.excerpt"
        :thumbnailUrl="post.thumbnailUrl"
        :date="post.date"
        :id="post.id"
      />
    </section>
  </div>
</template>

<script>
import ArticlePreview from "@/components/Blog/ArticlePreview"
import PodcastPreview from "@/components/Blog/PodcastPreview"
import moment from 'moment'

export default {
  components: {
        ArticlePreview,
        PodcastPreview
    },
  asyncData(context){
    return context.app.$storyapi
    .get(
      'cdn/stories', 
      {version: 'draft',
        starts_with:'blog/post-previews'
    })
    .then(res => {
      return {
        posts: res.data.stories.map(post => {
          return {        
            id: post.id,
            title: post.content.title,
            excerpt: post.content.excerpt,
            thumbnailUrl: post.content.thumbnailUrl.filename,
            date: moment(post.created_at).format('MMMM DD[,] YYYY')
          };
        })
      }
    })
  }
}
</script>


<style scoped>
.timeline-container {
  display: flex;
  min-height: 100vh;
  flex-flow: row nowrap;
  justify-content: space-evenly;
  align-items: flex-start;
  overflow-y: scroll;
  position: relative;
  padding-top: 8rem;
}
.middle-line {
  position: absolute;
  min-height: 100%;
  width: 3px;
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
