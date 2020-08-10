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
        >
        <div :style="{
            backgroundImage: `url(${require('../../assets/images/twitter.svg')})`,
          }"></div>
        <h1>ShaelynEOM</h1></a>
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="instagram"
          
        >
        <div :style="{
            backgroundImage: `url(${require('../../assets/images/instagram.svg')})`,
          }"></div>
        <h1>ShaelynEOM</h1></a>
        <a
          class="social-media-icon"
          rel="noreferrer noopener"
          target="_blank"
          :href="linkedin"
          
        >
                <div :style="{
            backgroundImage: `url(${require('../../assets/images/linkedin.svg')})`,
          }"></div>
        <h1>ShaelynOtikor</h1>
        </a>
      </div>
    </div>
    <div class="summary-container">
      <img class="profile-photo" :src="photo" />
      <div  class="profile-summary">
        <div v-for="(text, index) in richtext" :key="index" v-html="text">{{ summary }}</div>
        <a :href="`https://a.storyblok.com/f/88141/x/1f5db0b230/shaelyn-otikor-miller-speaker-profile.pdf`" class="pdf-link"> <div :style="{
            backgroundImage: `url(${require('../../assets/images/pdf-icon.png')})`,
          }"></div><h6>View/Print Short Bio Here</h6></a>
         <a
          class="social-media-icon-email"
          rel="noreferrer noopener"
          target="_blank"
          :href="`mailto:${gmail}`"
          
        >
                        <div :style="{
            backgroundImage: `url(${require('../../assets/images/gmail.svg')})`,
          }"></div>
        <h1>{{gmail}}</h1></a>
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
  justify-self: center;
  margin-bottom: 0;
  background-color: black;
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

.social-media-container a:hover {
transform: scale(1.1);
font-weight: bold;
}

.social-media-icon {
  height: 50px;
  width: 50px;
  display: flex;
  align-items: center;
  text-decoration: none;
  justify-content: space-between;
  flex-flow: column nowrap;
  margin: 0 1rem;
  
}



.social-media-icon div{
    height: 36px;
  width: 36px;
   background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  background-color: none;
}

.social-media-icon h1 {
  color: black;
  font-size: 1rem;
}

.summary-container {
  padding: 0;
  background-color: black;
  width: 100%;
  max-width: 1440px;
  justify-self: flex-end;
  color: white;
  height: 100%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: center;
}

.pdf-link{
  color: wheat;
  width: 100%;
  display: flex;
  font-family: 'Dosis', sans-serif;
  align-items: center;
}

.pdf-link:active, .pdf-link:visited {
  color: rgb(194, 175, 139);
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
  position: relative;
}

.social-media-icon-email {
  color: wheat;
  display: flex;
  align-items: center;
  padding-bottom: 1rem;
}

.social-media-icon-email:active, .social-media-icon-email:visited{
  color: rgb(194, 175, 139);
}


.social-media-icon-email div:hover, .pdf-link div:hover {
  transform: scale(1.1);
}
.social-media-icon-email div, .pdf-link div {
  height: 36px;
  max-width: 36px;
  margin: 0 1rem;
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  background-color: none;
}
.social-media-icon-email h1 {
  font-size: 1.4rem;
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

@media only screen and (orientation: Portrait) and (max-width: 320px){
  .social-media-icon-email h1, .pdf-link {
  font-size: 1.2rem;
}

}


/* Mobile Landscape */
@media only screen and (orientation: Landscape) and (min-width: 550px) {
  .summary-container {
    display: block;
    height: 100%;
  }
.profile-name{
  font-size: 3rem;
}
  .profile-photo {
    float: left;
    max-width: 40%;
    margin-right:3rem;
    margin-bottom: 1.5rem;
    shape-outside: inset() margin-box;
      border: 1px solid white;
  }
  .profile-summary {
    border: 1px solid white;
    width: 100%;
    text-align: justify;
  }

  .profile-summary div {
    line-height: 1.4;
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

   .social-media-icon-email h1, .pdf-link {
  font-size: 1.4rem;
}

}

/* Large Phone Landscape */
@media only screen and (orientation: Landscape) and (min-width: 810px) {
  .about-container {
    max-width: 100%;
  }

.profile-summary, .social-media-icon-email h1, .pdf-link{
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
   .social-media-icon-email h1, .pdf-link{
     font-size: 2rem;
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

.social-media-icon-email h1, .pdf-link {
  font-size: 2rem;
}
}
</style>
