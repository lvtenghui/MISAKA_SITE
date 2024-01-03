<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import MainPage from './components/LoginPage/MainPage.vue'
// import TestPage from './components/TESTPlace/testpage.vue'
</script>

<template>
  <!--暂时测试隐藏-->
  <MainPage></MainPage>

  <!--测试页面，用于学习下翻页面-->
  <!-- <TestPage></TestPage> -->

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
