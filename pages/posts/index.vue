<template>
  <div class="timeline-container">
    <section class="left-container">
    
    </section>
    <span class="middle-line"></span>
    <section class="right-container">
        <div class="post-container" v-for="post in posts" :key="post.id">
          <div class="line-point">
            <i class="arrow right" />
            <span class='line'>
            <h2 class="date">{{post.date}} </h2>
            </span>
            <span class="dot" />
          </div>
          <nuxt-link tag='article' :to="post.id" class="preview-container right-side">
              <div class="preview-thumbnail" :style="{backgroundImage: `url(${post.thumbnailUrl})`}"></div>
              <div class="preview-content">
                <h1 class="preview-title">{{post.title}}</h1>
                <p class="preview-text">{{post.excerpt}}</p>
              </div>
          </nuxt-link>
        </div>
    </section>
  </div>
</template>

<script>
export default {
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
  border: 1px solid red;
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
  height: 100vh;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;

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
  width: 40%;
  height: 16px;
  display: flex;
  align-self: flex-end;
  flex-flow: row-reverse nowrap;
  align-items: center;
  justify-content: flex-end;
  position: absolute;
  top: -8px;
  left: -8px;
}
.line {
  border: 1px solid white;
  color: white;
  background-color: white;
  width: 100%;
  height: 2px;
  display: flex;
  justify-content: center;
}

.date {
  position: absolute;
  top: -10px;
  font-size: 16px;
}

.arrow {
  border: solid white;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;

}

.left {
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
}
.right {
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
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
.preview-container {
  text-decoration: none;
  width: 50%;
  height: 50vh;
  border: 1px solid white;
  display: flex;
  margin: 2.5% 5%;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
}

.right-side {
  align-self: flex-end;
}

.left-side {
  align-self: flex-start;
}

.preview-thumbnail {
  background-position: center;
  background-size: cover;
  width: 100%;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  height: 75%;
}

.preview-content {
  display: flex;
  flex-flow: column nowrap;
  padding: 2.5%;
  width: 100%;
  height:25%;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  background: white;
  color: black;
}

.preview-title {
  font-size: 1.8rem;
}

.preview-text {
  font-size: 1.4rem;
}

@media (min-width: 35rem) {
  .post-preview {
    width: 25rem;
  }
}
</style>