<template>
  <section class="about-container">
    <h1 class="profile-name">{{ name }}</h1>
    <div class="summary-container">  
      <img class="profile-photo" :src="photo" />
      <p class="profile-summary">{{ summary }}</p>
      <div class="social-media-container">
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="twitter"
          :style="{
            backgroundImage: `url(${require('../../assets/images/twitter.svg')})`,
          }"
        ></a>
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="instagram"
          :style="{
            backgroundImage: `url(${require('../../assets/images/instagram.svg')})`,
          }"
        ></a>
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="linkedin"
          :style="{
            backgroundImage: `url(${require('../../assets/images/linkedin.svg')})`,
          }"
        ></a>
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="`mailto:${gmail}`"
          :style="{
            backgroundImage: `url(${require('../../assets/images/gmail.svg')})`,
          }"
        ></a>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories/about', { version: 'draft' })
      .then((res) => {
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
  },
}
</script>

<style scoped>
.about-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: stretch;
  align-items: center;
  margin-top: 6rem;
  margin-bottom: 0;
  background-color: black;
}
.summary-container {
  padding: 2rem 4rem 0;
  background-color: black;
  width: 65%;
  justify-self: flex-end;
  color: white;
  height: calc(100vh - 12.5rem);
  border-left: 1px solid white;
  border-right: 1px solid white;
  border-bottom: 1px solid white;
  position: relative;
}
.profile-name {
  font-size: 4rem;
  text-align: center;
  font-family: 'Dosis', sans-serif;
  padding: 1rem;
  color: black;
  background-color: white;
  width: 100%;
  height: 6rem;
}
.profile-photo {
  height: auto;
  float: left;
  shape-outside: inset() content-box;
  max-width: 100%;
  margin-right: 2rem;
}
.profile-summary {
  font-family: 'Lato', sans-serif;
  font-size: 2.4rem;
  width: 100%;
  line-height: 1.5;
  text-align: justify;
}
.social-media-container {
  width: 30%;
  z-index: 10;
  float: right;
  height: 100px;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
  align-items: center;
  position: absolute;
  bottom: 0;
  right: 0;
}

.social-media-icon {
  height: 36px;
  width: 36px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-color: white;
  border: 1px solid white;
  border-radius: 50%;
}
</style>
