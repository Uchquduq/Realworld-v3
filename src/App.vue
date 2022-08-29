<template>
  <nav>
    <div class="flashMessage" v-if="GStore.flashMessage">
      {{ GStore.flashMessage }}
    </div>
    <router-link
      class="mb-2 text-1xl font-bold tracking-tight text-gray-900"
      :to="{ name: 'EventList' }"
      >Events</router-link
    >
    |
    <router-link
      class="mb-2 text-1xl font-bold tracking-tight text-gray-900"
      to="/about"
      >About</router-link
    >
  </nav>
  <router-view />
</template>

<script>
export default {
  name: "App",
  inject: ["GStore"],
};
</script>

<style lang="scss">
@keyframes yellowfade {
  from {
    background: yellow;
  }
  to {
    background: transparent;
  }
}

.flashMessage {

  margin: 10px;
  padding: 5px;
  animation-name: yellowfade;
  animation-duration: 3s;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

h4 {
  font-size: 20px;
}
</style>
