<template>
  <div>
    <p>Register for the event here</p>
    <button @click="register">Register Me</button>
  </div>
</template>

<script>
export default {
  name: "EventDetails",
  props: ['event'],
  methods: {
    register() {
      this.$router.push({
        name: 'EventDetails'
      })
    }
  }
};
</script>
