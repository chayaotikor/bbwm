<template>
     <div class="post-container">
          <div class="line-point">
            <i class="right-arrow" />
            <span class='line'>
            <h2 class="date">{{date}}</h2>
            </span>
            <span class="dot" />
          </div>
          <nuxt-link tag='article' :to="`/posts/${id}`" class="preview-container">
              <div class="preview-thumbnail" :style="{backgroundImage: `url(${thumbnailUrl})`}"></div>
              <div class="preview-content">
                <h1 class="preview-title">{{title}}</h1>
                <p class="preview-text">{{excerpt}}</p>
              </div>
          </nuxt-link>
        </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            required: true
        },
        excerpt: {
            type: String,
            required: true
        },
        thumbnailUrl: {
            type: String,
            required: true
        },
        id: {
            type: Number,
            required: true
        },
        date: {
            type: String,
            required: true
        },
    }
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
  width: 47.5%;
  height: 16px;
  display: flex;
  align-self: flex-end;
  flex-flow: row-reverse nowrap;
  align-items: center;
  justify-content: flex-end;
  position: absolute;
  top: -8px;
  left: -6px;
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

.right-arrow {
  border: solid white;
  border-width: 0 3px 3px 0;
  display: inline-block;
  padding: 3px;
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
  height: 45vh;
  border: 1px solid white;
  display: flex;
  margin: .5% 2% 2%;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  cursor: pointer;
  align-self: flex-end;
}


.preview-thumbnail {
  background-position:top;
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

</style>
