<script>
import NavBar from './NavBar.vue'
import EarthBackground from './EarthBackground.vue';
import Logo from './Logo.vue';
import Login from './Login.vue';
import Register from './Register.vue';
import { ref } from 'vue';

export default {
    components: {
        NavBar,
        EarthBackground,
        Logo,
        Login,
        Register
    },
    setup() {
        const LogoFunction = ref(true);
        const LoginFunction = ref(false);
        const RegisterFunction = ref(false);

        const clickLogin = () => {
            LogoFunction.value = false;
            LoginFunction.value = true;
            RegisterFunction.value = false;
        };

        const clickRegister = () => {
            LogoFunction.value = false;
            LoginFunction.value = false;
            RegisterFunction.value = true;
        };

        const clickLogo = () => {
            LogoFunction.value = true;
            LoginFunction.value = false;
            RegisterFunction.value = false;
        };

        return {
            LogoFunction,
            LoginFunction,
            RegisterFunction,
            clickLogin,
            clickRegister,
            clickLogo
        };
    }
};
</script>

<template>
    <NavBar></NavBar>
    <div id="MainPage" class="row"
        style="text-align: center; height: 100vh; width: 100%;--bs-gutter-x: 0;user-select: none;">
        <EarthBackground style="z-index: 1;"></EarthBackground>
        <div v-if="LogoFunction" style="z-index: 2;vertical-align: middle;margin: auto;width: 100%;">
            <Logo></Logo>
            <div class="col col-xl-12 col-xxl-6 offset-xxl-6" style="margin-top: 100px;">
                <button type="button" class="btn btn-outline-warning btn-lg" @click="clickLogin">登录/注册</button>
            </div>
        </div>
        <div v-if="LoginFunction" style="z-index: 2;vertical-align: middle;margin: auto;width: 100%;">
            <Login></Login>
            <div class="col col-xl-12 col-xxl-6 offset-xxl-6" style="margin-top: 100px;">
                <button type="button" class="btn btn-outline-warning btn-lg" @click="clickLogo">返回首页</button>
            </div>
        </div>
        <div v-if="RegisterFunction" style="z-index: 2;vertical-align: middle;margin: auto;width: 100%;">
            <Register></Register>
            <div class="col col-xl-12 col-xxl-6 offset-xxl-6" style="margin-top: 100px;">
                <button type="button" class="btn btn-outline-warning btn-lg" @click="clickLogin">返回登录</button>
            </div>
        </div>
    </div>
</template>
