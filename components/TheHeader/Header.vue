<template>
  <header class="main-header">
    <nav class="main-nav">
      <div class="site-logo">
        <span
          :style="{
            backgroundImage: `url(${require('../../assets/images/icon.png')})`,
          }"
        />
        <h1>Beyond Boundaries | Without Measures</h1>
      </div>
      <ul class="nav-links">
        <nuxt-link tag="li" exact to="/" class="nav-link">
          <a>Home</a>
        </nuxt-link>
        <nuxt-link tag="li" to="/blog/posts" class="nav-link">
          <a>Posts</a>
        </nuxt-link>
        <nuxt-link tag="li" to="/about" class="nav-link">
          <a>About</a>
        </nuxt-link>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
.main-header {
  position: fixed;
  top: 0;
  left: 0;
  height: 6rem;
  background-color: black;
  width: 100%;
  display: flex;
  flex-flow: row nowrap;
  justify-content: flex-end;
  align-items: center;
  border-bottom: 1px solid white;
  z-index: 100;
}

.main-nav {
  height: 6rem;
  width: 100%;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;
  align-items: center;
}

.nav-links {
  width: 40%;
  display: flex;
  padding: 2.5%;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
  align-items: center;
}

.nav-link.nuxt-link-exact-active {
  font-weight: bold;
}

.nav-link a {
  text-decoration: none;
  color: white;
  font-family: 'Dosis', sans-serif;
  font-size: 1.4rem;
}

.nav-link a:hover,
.nav-link a:active,
.nav-link.nuxt-link-exact-active a {
  color: wheat;
}
.site-logo {
  display: flex;
  justify-content: flex-start;
  padding: 1%;
  width: 60%;
  align-items: center;
}

.site-logo h1 {
  font-size: 1.4rem;
  text-align: left;
  color: white;
  font-weight: bold;
  font-family: 'Economica', sans-serif;
}

.site-logo span {
  margin-right: 1%;
  height: 24px;
  min-width: 24px;
  background-position: center;
  background-size: cover;
}

@media only screen and (max-width: 320px) {
  .nav-link a {
    font-size: 1rem;
  }
  .site-logo h1 {
    font-size: 1rem;
  }
}

@media only screen and (min-width: 812px) {

   .nav-link a {
    font-size: 2rem;
  }
    .site-logo h1 {
    font-size: 2rem;
  }
}



</style>
