<template>
  <header class="header">
    <img src="../assets/header-bg.jpg" class="header-image">
    <!-- <h1 class="logo">The Rick and Morty API</h1> -->
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  position: relative;
  width: 100%;
}

.header-image {
  width: 100%;
  height: 50vh; 
  object-fit: cover;
}

.logo {
  font-size: 2rem;
  position: absolute;
  top: 10%;
  left: 10%;
  transform: translate(-10%, -10%);
  z-index: 1;
  color: whitesmoke;
}
</style>
