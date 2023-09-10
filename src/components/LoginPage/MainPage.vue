<script setup>
import NavBar from './NavBar.vue'
import EarthBackground from './EarthBackground.vue';
</script>

<template>
    <NavBar></NavBar>
    <div class="row" style="text-align: center; height: 100vh; width: 100%;--bs-gutter-x: 0;">
        <EarthBackground style="z-index: 1;"></EarthBackground>
        <div style="vertical-align: middle;margin: auto;z-index: 2;">
            <div class="col-12" style="margin-top: 20px;">
                <img src="../../assets/logo.png" alt="Logo" width="calc(50vw)">
            </div>
            <div class="col-12" style="margin-top: 100px;">
                <b style="font-size: 3.5em; color: white;">XFlySim 全球连线飞行平台</b>
            </div>
        </div>
    </div>
    
</template>
