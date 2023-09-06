<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import LoginPage from './components/LoginPage.vue'
</script>

<template>
  <LoginPage style="width: 100vw; height: 100vh;"></LoginPage>
  <!-- <HelloWorld msg="Vite + Vue" /> -->
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
