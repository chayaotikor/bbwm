<template>
  <section class="about-container" v-editable="blok">
    <div class="top-bar">
      <h1 class="profile-name">{{ heading }}</h1>
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
      <div  class="profile-summary">
        <div v-for="(text, index) in richtext" :key="index" v-html="text">{{ summary }}</div>
        </div>
    </div>
  </section>
</template>
<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get('cdn/stories/about', {
        version: process.env.NODE_ENV == 'production' ? 'published' : 'draft',
      })
      .then((res) => {
        return {
          blok: res.data.story.content,
          heading: res.data.story.content.heading,
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
     const textArr = this.summary.content.map(text => {
      return text
        ? this.$storyapi.richTextResolver.renderNode(text)
        : ''
      })
      return textArr

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
  background: none;
}

.top-bar {
  background-color: white;
  width: 100%;
  height: 6rem;
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: center;
}
.profile-name {
  font-size: 2rem;
  text-align: left;
  font-family: 'Dosis', sans-serif;
  padding: 1rem;
  font-weight: bold;
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
  max-width: 1440px;
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
  width: 100%;

}
.profile-summary {
  font-family: 'Lato', sans-serif;
  font-size: 1.4rem;
  width: 100%;
  line-height: 1.2;
  text-align: left;
  border: 1px solid white;

}

.profile-summary div {
  padding: 1rem;
}

@media only screen and (orientation: Portrait) and (max-width: 240px) and (max-height: 320px) {
  .profile-name {
    font-size: 1.2rem;
  }
  .social-media-icon {
    height: 1.8rem;
    width: 1.8rem;
  }
}



/* Mobile Landscape */
@media only screen and (orientation: Landscape) and (min-width: 550px) {
  .summary-container {
    flex-flow: row nowrap;
    align-items: stretch;
    justify-content: center;
    height: 100%;
  }
.profile-name{
  font-size: 3rem;
}
  .profile-photo {
    width: 45%;
      border: 1px solid white;
  }
  .profile-summary {
    border: 1px solid white;
    line-height: 1.1;
    width: 55%;
  }
}


/* Tablet Portrait */
 @media only screen and (orientation: Portrait) and (min-width: 768px) {
   .about-container{
     width: 70vw;
   }
   .profile-photo{
     border: 1px solid white;
   }
   .profile-summary{
     font-size: 1.6rem;
   }
   .profile-name {
     font-size: 3rem;
   }
}

/* Large Phone Landscape */
@media only screen and (orientation: Landscape) and (min-width: 810px) {
  .about-container {
    max-width: 100%;
  }

.profile-summary{
  font-size: 1.6rem;
}
}

/* Tablet Landscape */
@media only screen and (min-width: 1024px) {


  .profile-summary {
    padding: 1rem;
    font-size: 2rem;
    line-height: 1.5;
  }
}

/* Laptops and Large Tablets */

@media only screen and (min-width: 1280px) {
  .profile-summary {
    line-height: 2;
  }
}

/* Large Screens */
@media only screen and (min-width: 1440px) {

.profile-summary{
  font-size: 2.8rem;
  line-height: 1.5;
}
}
</style>
