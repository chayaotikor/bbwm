<template>
  <header class="main-header">
    <nav class="main-nav">
      <ul class="nav-links">
        <nuxt-link tag="li" to='/home' class="nav-link">
          <a>Home</a>
        </nuxt-link>
        <nuxt-link tag="li" to="/posts" class="nav-link">
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
  top:0;
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
display:flex;
flex-flow: row nowrap;
justify-content: flex-end;
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

 .nav-link a:hover, .nav-link a:active, .nav-link.nuxt-link-exact-active a {
  color: wheat;
}
/* Mobile Landscape */
@media only screen and (min-width: 576px) {

}

/* Tablet Portrait */
@media only screen and (min-width: 768px) {

}

/* Tablet Landscape */
@media only screen and (min-width: 810px) {


}

/* Desktop */
@media only screen and (min-width: 1024px) {

}

</style>