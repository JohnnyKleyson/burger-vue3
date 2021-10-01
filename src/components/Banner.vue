<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
  </div>
</template>

<script>
export default {
  name: "Banner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/img/burger.jpg");
  background-position: 0 -250px;
  background-size: cover;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  color: white;
}
#main-banner h1{
color: white;
text-align: center;
font-size: 3.5rem;
background-color: #222;
padding: 20px 40px;
}
</style>
