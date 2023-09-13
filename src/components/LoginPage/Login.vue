<template>
    <div class="col col-xl-12 col-xxl-6 offset-xxl-6" style="margin-top: 20px;">
        <div class="login-box">
            <h2>Login</h2>
            <div class="login-input-box">
                <label>账号</label>
                <input type=""/>
            </div>
            <div class="login-input-box">
                <label>密码</label>
                <input type="password"/>
            </div>
            <div class="login-btn-box">
                <a href="#">忘记密码?</a>
                <div>
                    <button>登录</button>
                    <button>注册</button>
                </div>
            </div>
        </div>
    </div>
</template>


<style>
.login-box{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.login-box > h2{
    color: rgba(255,255,255,0.9);
    margin-bottom: 20px;
}

.login-box .login-input-box{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: start;
    margin-bottom: 10px;
}
.login-box .login-input-box > label{
    margin-bottom: 5px;
    color: rgba(255,255,255,0.9);
    font: 1em;
}
.login-box .login-input-box > input{
    color: rgba(255,255,255,0.9);
    font: 1em;
    background: rgba(255,255,255,0.3);
    border: 1px solid rgba(255,255,255,0.5);
    border-radius: 5px;
    transition: 0.2s;
    height: 35px;
    font-size: 14px;
    outline: none;
    padding: 0 10px;
}
.login-box .login-input-box > input:focus{
    border: 1px solid rgba(255,255,255,0.8);
}
.login-box .login-btn-box{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: start;
}
</style>