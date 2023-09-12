<script setup>
import NavBar from './NavBar.vue'
import EarthBackground from './EarthBackground.vue';
import Logo from './Logo.vue';
import Login from './Login.vue';
</script>

<template>
    <NavBar></NavBar>
    <div class="row" style="text-align: center; height: 100vh; width: 100%;--bs-gutter-x: 0;user-select: none;">
        <EarthBackground style="z-index: 1;"></EarthBackground>
        <Logo style="z-index: 2;"></Logo>
        <Login style="z-index: 2;"></Login>
    </div>
    
</template>
