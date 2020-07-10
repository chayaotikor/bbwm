<template>
  <section class="about-container" v-editable="blok">
    <div class="top-bar">
    <h1 class="profile-name">{{ name }}</h1>
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
    <div class="summary-container">
      <img class="profile-photo" :src="photo" />
      <p v-html="richtext" class="profile-summary">{{ summary }}</p>
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
          blok: res.data.story.content,
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
  computed: {
    richtext() {
      return this.summary
        ? this.$storyapi.richTextResolver.render(this.summary)
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
.about-container {
  display: flex;
  flex-flow: column nowrap;
  justify-content: stretch;
  align-items: center;
  margin-top: 6rem;
  justify-self: center;
  margin-bottom: 0;
  background-color: black;
  max-width: 100%;
}


.top-bar{
  background-color: white;
  width: 100%;
  height: 6rem;
  position: relative;
display: flex;
justify-content: space-around;
align-items: center;
}
.profile-name {
  font-size: 3rem;
  text-align: left;
  font-family: 'Dosis', sans-serif;
  padding: 1rem;
  color: black;

}

.social-media-container {
   max-width: 100%;
  z-index: 10;
  height: auto;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
  align-items: center;

}

.social-media-icon {
  height: 36px;
  width: 36px;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-color: none;
  border-radius: 50%;
  margin: 0 1rem;
}

.summary-container {
  padding: 0;
  background-color: black;
  width: 100%;
  justify-self: flex-end;
  color: white;
  height: calc(100vh + 6rem);
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

.profile-photo {
  height: auto;
  max-width: 100%;
  width: 65%;
}
.profile-summary {
  font-family: 'Lato', sans-serif;
  font-size: 1.4rem;
  width: 100%;
  border-top: 1px solid white;
  line-height: 1.2;
  padding: 1rem;
  text-align: left;
}

/* Mobile Landscape */
@media only screen and (min-width: 576px) {
  .summary-container {
    flex-flow: row nowrap;
    align-items: stretch;
    height: 100vh;
  }

  .profile-photo {
    width: 50%;
  }
  .profile-summary {
    border: none;
    padding: 0 1rem;
    line-height: 1.1;
  }
}

/* Tablet Portrait */
@media only screen and (min-width: 768px) {
  .about-container{
    border-left: 1px solid white;
    border-right: 1px solid white;
  }
  .summary-container {
    display: block;
    height: 80vh;
    border-bottom: 1px solid white;
  }
  
  .profile-photo{
    float: left;
    margin: 1rem 1rem 0;
    shape-outside: inset() content-box;
    border: 1px solid white;

  }
  .profile-summary{
    padding: 1rem;
    font-size: 1.6rem;
    line-height: 1.5;
  }
}

/* Large Phone Landscape */
@media only screen and (min-width: 810px) {
  .about-container{
    max-width:100%;
  border: none;
  }

  .summary-container{
    border: none;
  }
}


/* Tablet Landscape */
@media only screen and (min-width: 1024px) {
  .about-container{
    max-width:800px;
    border: 1px solid white
  }


  .profile-summary{
    padding: 1rem;
     font-size: 1.8rem;
    line-height: 1.5;
  }
}
@media only screen and (min-width: 1280px){
 .about-container{
   height: 100vh;
 }

 .summary-container{
   border:none
 }
}

</style>
