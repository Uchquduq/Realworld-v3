<template>
  <h1>Uh-Oh!</h1>
  <h3>
    It looks like you're expiriencing some network issues, please take a breathe
    and <a href="#" @click="$router.go(-1)">click here</a> to try again.
  </h3>
</template>

<script>
export default {
  name: "NetworkError",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
