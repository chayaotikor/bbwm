<template>
     <div class="post-container">
          <div class="line-point">
            <i class="right-arrow" />
            <span class='line'>
            <!-- <h2 class="date">{{date}}</h2> -->
            </span>
            <span class="dot" />
          </div>
          <nuxt-link tag='article' :to="`/blog/posts/${id}`" class="preview-container">
              <div class="preview-thumbnail" :style="{backgroundImage: `url(${image})`}"></div>
              <div class="preview-content" >
                <h1 class="preview-title">{{title}}</h1>
                <div class="preview-text" v-html="richtext">{{excerpt}}</div>
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
            type: Object,
            required: true
        },
        image: {
            type: String,
            required: true
        },
        id: {
            type: String,
            required: true
        },
        date: {
            type: String,
            required: true
        },
    },
       computed: {
    richtext() {
      return this.excerpt ? this.$storyapi.richTextResolver.render(this.excerpt) : ''
    }
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
  width: 100%;
  height: 16px;
  display: flex;
  align-self: flex-end;
  flex-flow: row-reverse nowrap;
  align-items: center;
  justify-content: flex-end;
  position: absolute;
  top: -8px;
  left: -5px;
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
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 1px solid white;
  background: white;
  margin: 0;
  z-index: 1;
}
.preview-container {
  text-decoration: none;
  width: 90%;
  height: 30vh;
  border: 1px solid white;
  display: flex;
  margin: 5%;
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
  height: 60%;
}

.preview-content {
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  padding: 2% 2.5%;
  width: 100%;
  height:50%;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
  background: white;
  color: black;

}

.preview-title {
  font-size: 1.2rem;
  font-weight: bold;
}

.preview-text {
  font-size: 1rem;
  text-align: justify;
}

@media only screen and (max-width: 320px) and (max-height: 320px){
  .preview-title{
    font-size: .8rem;
  }
  .preview-text{
    font-size: .6rem;
  }
}


/* Tablet Portrait */
@media only screen and (orientation: Portrait) and (min-width: 768px){

  .preview-title{
    font-size: 2.2rem;
    margin-bottom: 1rem;
  }

  .preview-text{
    font-size: 1.8rem;

  }
}

/* Tablet Landscape */
@media only screen and (orientation: Landscape) and (min-width: 1024px){
  .preview-title{
    font-size: 2.4rem;
    margin-bottom: .5rem;
  }

  .preview-text{
    font-size: 2rem;

  }

}

/* Large Tablet Portrait*/
@media only screen and (orientation: Portrait) and (min-width: 1024px){
    .preview-title{
    font-size: 2.4rem;
  }

  .preview-text{
    font-size: 2rem;

  }
}

/* Large Tablet Landscape*/
@media only screen and (orientation: Landscape) and (min-width: 1280px){
  .preview-container{
    width: 70%;
  }

  .preview-thumbnail{
    background-position: center;
  }
      .preview-title{
    font-size: 2.6rem;
  }

  .preview-text{
    font-size: 2.2rem;
  }
}
/* Desktop */


</style>
