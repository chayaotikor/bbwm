<template>
    <nuxt-link :to="id">
        <article class="post-preview">
            <div class="preview-thumbnail" :style="{backgroundImage: `url(${thumbnailUrl})`}"></div>
            <div class="preview-content">
                <h1 class="preview-title">{{title}}</h1>
                <p class="preview-text">{{excerpt}}</p>
            </div>
        </article>
      </nuxt-link>
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
        }

    }
}
</script>

<style scoped>
a {
    text-decoration: none;

}

.post-preview {
    border: 1px solid black;
    border-radius: 10px;
}

.preview-thumbnail {
background-position: center;
background-size: cover;
width: 100%;
height: 10rem;
}

.preview-content{
border: 1px solid red;
display: flex;
flex-flow: column nowrap;
padding: 2.5%;

}

.preview-title {
font-size: 1.8rem;
}

.preview-text {
font-size: 1.4rem;
}

@media (min-width: 35rem) {
    .post-preview {
        width: 25rem;
    }
}
</style>