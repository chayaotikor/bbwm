<template>
  <div class="posts-container">
    <section class="left-container">
      <div class="point-container" v-for="post in posts" :key="post.id">
        <div class="line-point">
          <span class="dot" />
          <span class="line" />
        </div>
        <PostPreview
          :title="post.title"
          :excerpt="post.excerpt"
          :thumbnailUrl="post.thumbnailUrl"
          :id="post.id"
        />
      </div>
    </section>
    <span class="middle-line"></span>
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
  height: 100vh;
  flex-flow: row nowrap;
  justify-content: space-evenly;
  align-items: center;
  /* overflow-y: scroll; */
  border: 1px solid white;
  position: relative;
}
.middle-line {
  position: absolute;
  height: 100vh;
  border: 2px solid white;
}

.left-container {
  width: 50%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
}

.right-container {
  width: 50%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: flex-end;
}
.point-container {
  border: 1px solid red;
  width: 100%;
  display: flex;
  flex-flow: row-reverse nowrap;
  justify-content: space-between;
  align-items: flex-start;
  position: relative;
}

.line-point {
  width: 50%;
  border: 1px solid blue;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  justify-content: flex-end;
  position: relative;
}
.line {
  border: 1px solid white;
  background-color: white;
  width: 100%;
  height: 2px;
  position: absolute;
  top: 0;
}

.dot {
  height: 16px;
  width: 16px;
  border-radius: 50%;
  border: 1px solid white;
  background: white;
  margin: 0;
  position: absolute;
  top: 0;
  right: -7.25%;
  -ms-transform: translateY(-50%);
  transform: translateY(-50%);
  z-index: 1;
}
</style>