<template>
  <h1>Oops!</h1>
  <h3>The {{ resource }} you're looking for is not here.</h3>
  <router-link :to="{ name: 'EventList' }">Back to home page</router-link>
</template>

<script>
export default {
  name: "NotFound",
  props: {
    resource: {
      type: String,
      required: true,
      default: "page",
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
