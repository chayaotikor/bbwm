<template>
  <header class="main-header">
    <div class="site-logo">
      <span
        :style="{
          backgroundImage: `url(${require('../../assets/images/icon.png')})`,
        }"
      />
      <h1>Beyond Boundaries | Without Measures</h1>
    </div>
    <div
      class="button-container"
      @click="open === true ? openMenu(false) : openMenu(true)"
    >
      <span
        class="menu-button"
        v-show="open === true"
        :style="{
          backgroundImage: `url(${require('../../assets/images/x-icon.png')})`,
        }"
      />
      <span
        v-show="open === false"
        class="menu-button"
        :style="{
          backgroundImage: `url(${require('../../assets/images/hamburger.png')})`,
        }"
      />
    </div>
    <nav class="main-nav" v-show="open === true">
      <ul class="nav-links"  @click="openMenu(false)">
        <nuxt-link tag="li" exact to="/" class="nav-link">
          <h1>Home</h1>
        </nuxt-link>
        <nuxt-link tag="li" to="/about" class="nav-link">
          <h1>About</h1>
        </nuxt-link>
        <nuxt-link tag="li" to="/blog/posts" class="nav-link">
          <h1>Posts</h1>
        </nuxt-link>
        <nuxt-link tag="li" to="/blog/appearances" class="nav-link">
          <h1>Appearances</h1>
        </nuxt-link>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  data: () => {
    return {
      open: false,
    }
  },

  methods: {
    openMenu(bool) {
      this.open = bool
    },
  },
}
</script>

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
  justify-content: center;
  align-items: center;
  border-bottom: 1px solid white;
  z-index: 50;
}

.main-nav {
  display: flex;
  justify-content: center;
}
.button-container {
  position: absolute;
  height: 6rem;
  right: 0;
  width: 25vw;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  background-color: none;
}
.menu-button {
  z-index: 85;
  height: 16px;
  width: 16px;
  margin: 1rem;
  background-position: center;
  background-size: cover;
}

.nav-links {
  width: 25vw;
  position: absolute;
  top: 6rem;
  right: 0;
  height: 50vh;
  z-index: 81;
  background: black;
  border-left: 2px solid white;
  border-bottom: 2px solid white;
  display: flex;
  padding: 2.5%;
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-evenly;
  align-items: center;
  -webkit-box-shadow: -200px 200px 300px 200px rgba(0, 0, 0, 0.5);
  -moz-box-shadow: -200px 200px 300px 200px rgba(0, 0, 0, 0.5);
  box-shadow: -200px 200px 300px 200px rgba(0, 0, 0, 0.5);
}

.nav-link.nuxt-link-exact-active {
  font-weight: bold;
}
.nav-link {
  width: 100%;
  height: 25%;
  display: flex;
  flex-flow: column nowrap;;
  justify-content: center;
  align-items: center;
  text-align: center;
  cursor: pointer;
}

.nav-link h1 {
  text-decoration: none;
  color: white;
  font-family: 'Dosis', sans-serif;
  font-size: 1.4rem;
  width: 100%;
}

.nav-link h1:hover,
.nav-link h1:active,
.nav-link.nuxt-link-exact-active h1 {
  color: wheat;
}
.site-logo {
  display: flex;
  justify-content: center;
  padding: 1%;
  width: 80%;
  height: 6rem;
  align-items: center;
}

.site-logo h1 {
  font-size: 1.8rem;
  text-align: center;
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
  .nav-link h1 {
    font-size: 1rem;
  }
  .site-logo h1 {
    font-size: 1.2rem;
  }
}

@media only screen and (min-width:640px) {
  .button-container {
    justify-content: center;
  }
}

@media only screen and (min-width: 768px) {
  .nav-link h1 {
    font-size: 2rem;
  }
  .site-logo h1 {
    font-size: 3rem;
  }
}


</style>
