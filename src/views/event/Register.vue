<template>
  <div>
    <p>Register for the event here</p>
    <button @click="register">Register Me</button>
  </div>
</template>

<script>
export default {
  name: "EventDetails",
  props: ["event"],
  inject: ["GStore"],
  methods: {
    register() {
      this.GStore.flashMessage =
        "You are succesfully registered for " + this.event.title;

      setTimeout(() => {
        this.GStore.flashMessage = "";
      }, 3000);

      this.$router.push({
        name: "EventDetails",
      });
    },
  },
};
</script>
