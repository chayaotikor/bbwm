<template>
    <div>
        <h1></h1>
        <p></p>
    </div>
</template>
<script>
export default {
    asyncData(context){
    return context.app.$storyapi
    .get(
      'cdn/stories/blog/posts' + context.params.postId, 
      {version: 'draft'
    })
    .then(res => {
        console.log('res', res.data.story.content)
      return {
      }
    })
  }
}
</script>
