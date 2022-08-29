<template>
  <div class="history">
    <button @click="$router.go(-1)">&#60;&#60; back</button>
    <button @click="$router.go(1)">forward &#62;&#62;</button>
  </div>

  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails' }">Details</router-link> |
      <router-link :to="{ name: 'EventRegister' }">Register</router-link> |
      <router-link :to="{ name: 'EventEdit' }">Edit</router-link>
    </div>
    <router-view :event="event"></router-view>
  </div>
</template>

<script>
import EventService from "@/services/EventService";
export default {
  name: "EventDetails",
  props: ["id"],
  data: () => ({
    event: null,
  }),
  created() {
    EventService.getEvent(this.id)
      .then((response) => (this.event = response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style lang="scss">
a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;

  &.router-link-exact-active {
    color: #42b983;
  }
}

.history button {
  margin: 3px;
  padding: 4px;
  background: #42b983;
  min-width: 80px;
}
button:hover {
  background: #4ace93;

}

</style>
