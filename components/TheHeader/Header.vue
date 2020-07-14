<template>
  <header class="main-header">
    <nav class="main-nav">
      <h1 class="site-logo">Beyond Boundaries | Without Measure</h1>
      <ul class="nav-links">
        <nuxt-link tag="li" to="/home" class="nav-link">
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
  width: 50%;
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
  font-size: 1.8rem;
}

.nav-link a:hover,
.nav-link a:active,
.nav-link.nuxt-link-exact-active a {
  color: wheat;
}
.site-logo {
  font-size: 3rem;
  padding: 2.5%;
  width: 50%;
  text-align: left;
  color: white;
  font-weight: bold;
  font-family: 'Economica', sans-serif;
}



@media only screen and (max-width: 640px) {
  .site-logo {
    font-size: 1.8rem;
  }
}

@media only screen and (max-width: 812px) {
  .site-logo {
    font-size: 2.4rem;
  }
}
@media only screen and (max-width: 320px) and (max-height: 320px) {
  .nav-link a {
    font-size: 1rem;
  }
  .site-logo {
    font-size: 0.8rem;
  }
}
</style>
