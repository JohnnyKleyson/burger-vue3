<template>
  <div>
    <h1 class="message-container">
      <p>{{msg}}</p>
    </h1>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
};
</script>

<style scoped>
.message-container {
  font-size: 1.1rem;
  text-transform: uppercase;
  color: #001085;
  background-color: #cce5ff;
  border: 2px solid #b8daff;
  border-radius: 5px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}
</style>
