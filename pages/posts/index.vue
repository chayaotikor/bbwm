<template>
  <div class="posts-container">
    <section class="left-container">
              <PostPreview
        v-for="post in posts"
        :key="post.id"
        :title="post.title"
        :excerpt="post.excerpt"
        :thumbnailUrl="post.thumbnailUrl"
        :id="post.id"
      />
    </section>
    <section class="right-container">
      <PostPreview
        v-for="post in posts"
        :key="post.id"
        :title="post.title"
        :excerpt="post.excerpt"
        :thumbnailUrl="post.thumbnailUrl"
        :id="post.id"
      />
    </section>
  </div>
</template>

<script>
import PostPreview from "@/components/Blog/PostPreview"
export default {
    components: {
        PostPreview
    },
    data(){
        return{
            posts: [
                {
                    id: 1,
                    thumbnailUrl: "https://www.rspcasa.org.au/wp-content/uploads/2019/01/Adopt-a-dog-or-puppy-from-RSPCA-South-Australia-749x1024.jpg",
                    title: "First Post",
                    excerpt: "This will be a preview or summary of the article"
                },
                             {
                    id: 2,
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
.posts-container {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-evenly;
    align-items: center;
    overflow-y: scroll;
    border: 1px solid white;
}
.left-container {
    border: 1px solid blue;
    width: 50%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: flex-start;
}

.right-container {
    border: 1px solid pink;
    width: 50%;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: flex-end;
}
</style>