<template>
    <section class="about-container">
        <h1 class="profile-name">{{name}}</h1>
       <div class="summary-container">
        <img class="profile-photo" :src="photo">
        <p class="profile-summary">{{summary}}</p>
        <div class="social-media-container">
            <a class="social-media-icon" rel="noreferrer noopener" target="_blank" :href="twitter" :style="{backgroundImage: `url(${require('../../assets/images/twitter.svg')})`}"></a>
            <a class="social-media-icon" rel="noreferrer noopener" target="_blank" :href="instagram" :style="{backgroundImage: `url(${require('../../assets/images/instagram.svg')})`}"></a>
            <a class="social-media-icon" rel="noreferrer noopener" target="_blank" :href="linkedin" :style="{backgroundImage: `url(${require('../../assets/images/linkedin.svg')})`}"></a>
            <a class="social-media-icon" rel="noreferrer noopener" target="_blank" :href="`mailto:${gmail}`" :style="{backgroundImage: `url(${require('../../assets/images/gmail.svg')})`}"></a>

        </div>
        </div>
    </section>
</template>
<script>
export default {
    asyncData(context){
    return context.app.$storyapi
    .get(
      'cdn/stories/about', 
      {version: 'draft'
    })
    .then(res => {
      return {
          name: res.data.story.content.name,
          photo: res.data.story.content.photo.filename,
          summary: res.data.story.content.summary,
          linkedin: res.data.story.content.linkedin.url,
          twitter: res.data.story.content.twitter.url,
          instagram: res.data.story.content.instagram.url,
          gmail: res.data.story.content.gmail.email,

      }
    })
  }
}
</script>

<style scoped>
.about-container {
    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: center;
    position: relative;
    padding-top: 6rem;
    height: 100vh;
    background-color: black;
}
.summary-container {
    padding: 1%;
    background-color: white;
    width: 50%;
    height: 100vh;
    position: relative;
}
.profile-name {
    font-size: 4rem;
    width: 100%;
    text-align: center;
    font-family: 'Dosis', sans-serif;
    padding: 1rem;
    color: black;
    background-color: white;
    width: 50%;

}
.profile-photo {
    height: auto;
    float: left;
    shape-outside: inset() content-box;
    max-width: 100%;
    margin-right: 2rem;
    border: 1px solid black;
    -webkit-box-shadow: 0px 0px 44px 2px rgba(0,0,0,0.6);
    -moz-box-shadow: 0px 0px 44px 2px rgba(0,0,0,0.6);
    box-shadow: 0px 0px 44px 2px rgba(0,0,0,0.6);
}
.profile-summary {
    font-family: 'Lato', sans-serif;
    font-size: 2rem;
    width: 100%;
    line-height: 1.2;
    text-align: justify;
}
.social-media-container {
    width: 30%;
    z-index: 10;
    float:right;
    height: 100px;
    display: flex;
    flex-flow:row nowrap;
    justify-content: space-around;
    align-items: center;
}

.social-media-icon {
   height: 36px;
    width: 36px;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
}
</style>