<template>
  <div class="post-container">
    <section
      class="post-jumbotron"
      :style="{ backgroundImage: `url(${image})` }"
    ></section>
    <h6 class="image-credit">{{ credit }}</h6>
    <h1 class="post-title">{{ title }}</h1>
    <p class="post-text">{{ text }}</p>
  </div>
</template>
<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories/' + context.params.postId, {
        version: 'draft',
      })
      .then((res) => {
        console.log('res', res.data.story)
        return {
          title: res.data.story.content.title,
          text: res.data.story.content.text,
          image: res.data.story.content.image.filename,
          credit: res.data.story.content.credit,
        }
      })
  },
}
</script>
<style scoped>
.post-container {
  display: flex;
  flex-flow: column nowrap;
  color: white;
  margin: 6rem 0;
}
.post-jumbotron {
width: 100%;
height: 400px;
background-size: cover;
background-position: center;
}

.image-credit {
  font-size: .8rem;
  width: 100%;
  text-align: right;
  padding: .5rem;
}
.post-title {
  font-size: 4rem;
  width: 100%;
  text-align: center;
}

.post-text{
  padding: 2rem;
  font-size: 1.8rem;
}
</style>
