<template>
  <div class="post-container" v-editable="post.blok" >
    <section
      class="post-jumbotron"
      :style="{ backgroundImage: `url(${post.image})` }"
    ></section>
    <h6 class="image-credit">{{ post.credit }}</h6>
    <h1 class="post-title">{{ post.title }}</h1>
    <div v-html="richtext" class="post-text">{{ post.text }}</div>
  </div>
</template>
<script>
export default {
  async asyncData(context) {
    const postData = await context.app.$storyapi.get(
      'cdn/stories/' + context.params.postId,
      {
        version: 'draft',
      }
    )
    const post = {
      blok: postData.data.story.content,
      title: postData.data.story.content.title,
      text: postData.data.story.content.text,
      image: postData.data.story.content.image.filename,
      credit: postData.data.story.content.credit,
    }
    return { post }
  },
  computed: {
    richtext() {
      return this.post.text
        ? this.$storyapi.richTextResolver.renderNode(this.post.text)
        : ''
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
  border-bottom: 1px solid white;
  display: flex;
  flex-flow: column nowrap;
  align-items: center;
  color: white;
  margin: 6rem 0;
}
.post-jumbotron {
  width: 100%;
  height: 400px;
  background-size: cover;
  background-position: center;
  border-bottom: 1px solid white;
}

.image-credit {
  font-size: 0.8rem;
  width: 100%;
  text-align: right;
  padding: 0.5rem;
}
.post-title {
  font-size: 4rem;
  width: 100%;
  text-align: center;
}

.post-text {
  padding: 2rem;
  font-size: 1.8rem;
  line-height: 1.2;
  text-align: justify;
}
/* Large Laptops */
@media only screen and (min-width: 576px) {
.post-text{
  width: 75%;
  
}
}



</style>
