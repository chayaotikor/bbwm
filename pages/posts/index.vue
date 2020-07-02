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
                    thumbnailUrl: "https://www.rspcasa.org.au/wp-content/uploads/2019/01/Adopt-a-dog-or-puppy-from-RSPCA-South-Australia-749x1024.jpg",
                    title: "First Post",
                    excerpt: "This will be a preview or summary of the article"
                },
                             {
                    id: 2,
                    date: "June 25, 2020",
                    thumbnailUrl: "https://www.rspcasa.org.au/wp-content/uploads/2019/01/Adopt-a-dog-or-puppy-from-RSPCA-South-Australia-749x1024.jpg",
                    title: "Second Post",
                    excerpt: "This will be a preview or summary of the article"
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
  justify-content: space-evenly;
  align-items: flex-start;
  overflow-y: scroll;
  position: relative;
  padding: 8rem 0;
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
  height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;

}

</style>
