<template>
  <div class="timeline-container">
    <!-- <section class="left-container">
      <PodcastPreview  v-for="post in posts" :key="post.id" :title="post.title"
          :excerpt="post.excerpt"
          :thumbnailUrl="post.thumbnailUrl"
          :date="post.date"
          :id="post.id"/>
    </section> -->
    <span class="middle-line" />
    <section class="right-container">
      <ArticlePreview  v-for="post in posts" :key="post.id" :title="post.title"
          :excerpt="post.excerpt"
          :thumbnailUrl="post.thumbnailUrl"
          :date="post.date"
          :id="post.id"/>
    </section>
  </div>
</template>

<script>
import ArticlePreview from "@/components/Blog/ArticlePreview"
import PodcastPreview from "@/components/Blog/PodcastPreview"
import image1 from '@/assets/images/image1.jpg'
import image2 from '@/assets/images/image2.jpg'

export default {
  components: {
        ArticlePreview,
        PodcastPreview
    },
    data(){
        return{
            posts: [
                {
                    id: 1,
                    date: "June 26, 2020",
                    thumbnailUrl: image1,
                    title: "Article Title",
                    excerpt: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip."
                },
                             {
                    id: 2,
                    date: "June 25, 2020",
                    thumbnailUrl: image2,
                    title: "Article Title",
                    excerpt: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip."
                }
            ]
        }
    }
}
</script>


<style scoped>
.timeline-container {
  display: flex;
  min-height: 100vh;
  flex-flow: row nowrap;
  justify-content: center;
  align-items: flex-start;
  overflow-y: scroll;
  position: relative;
  padding-top: 8rem;
}
.middle-line {
  position: absolute;
 left: 10%;
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
  width: 80%;
  min-height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

</style>
