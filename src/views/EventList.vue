<template>
  <div class="events">
    <h1>Events For Good</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
    <div class="pagination">
      <router-link
        :to="{ name: 'EventList', query: { page: page - 1 } }"
        id="page-prev"
        rel="prev"
        v-if="page != 1"
        >&#60; Prev</router-link
      >

      <router-link
        :to="{ name: 'EventList', query: { page: page + 1 } }"
        id="page-next"
        rel="next"
        v-if="hasNextPage"
        >Next &#62;</router-link
      >
    </div>
  </div>
</template>
<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import EventService from "@/services/EventService.js";
import { watchEffect } from "vue";

export default {
  name: "EventList",
  props: ["page"],
  components: {
    EventCard,
  },
  data: () => ({
    events: null,
    totalEvents: 0,
  }),
  created() {
    watchEffect(() => {
      this.events = null;
      EventService.getEvents(2, this.page)
        .then((response) => {
          this.events = response.data;
          this.totalEvents = response.headers["x-total-count"];
        })
        .catch(() => {
          this.$router.push({ name: "NetworkError" });
        });
    });
  },
  computed: {
    hasNextPage() {
      let totalPages = Math.ceil(this.totalEvents / 2);
      return this.page < totalPages;
    },
  },
};
</script>

<style>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pagination {
  display: flex;
  width: 290px;
}

.pagination a {
  flex: 1;
  text-decoration: none;
  color: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>
