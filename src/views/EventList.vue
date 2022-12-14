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
import NProgress from "nprogress";

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
  beforeRouteEnter(routeTo, routeFrom, next) {
    NProgress.start();
    EventService.getEvents(2, parseInt(routeTo.query.page) || 1)
      .then((response) => {
        next((comp) => {
          comp.events = response.data;
          comp.totalEvents = response.headers["x-total-count"];
        });
      })
      .catch(() => {
        next({ name: "NetworkError" });
      })
      .finally(() => {
        NProgress.done();
      });
  },
  beforeRouteUpdate(routeTo) {
    NProgress.start();
    EventService.getEvents(2, parseInt(routeTo.query.page) || 1)
      .then((response) => {
        this.events = response.data;
        this.totalEvents = response.headers["x-total-count"];
      })
      .catch(() => {
        return { name: "NetworkError" };
      })
      .finally(() => {
        NProgress.done(); 
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
