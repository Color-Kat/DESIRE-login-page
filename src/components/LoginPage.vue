<template>
    <div id="login-page" :style="{ backgroundImage: 'url(\'' + require('@/assets/images/bg.png') + '\')' }">
        <form @submit.prevent="submitHandler">
            <div class="left">
                <div class="left-text">
                    <h1 class="title">Desire<br>RolePlay</h1>
                    <h4 class="description">Лучший проект игровых<br> серверов за всю историю GTA V</h4>
                </div>
                <div class="blackout"></div>
                <img :src="require('@/assets/images/city_bg.png')" alt="city">
            </div>
            <div class="right">
                <div class="content">
                    <h1 class="form-title">Авторизация</h1>
                    <span class="form-description">
                        Если у вас уже существует аккаунт,<br> 
                        вы можете войти в него
                    </span>

                    <div class="form-inputs">
                        <input 
                            type="text" 
                            placeholder="Логин"
                            v-model="login"
                            
                            id="login"
                        >
                        <input
                            type="password"
                            placeholder="Пароль"
                            v-model="password"
                            id="password"
                        >
                    </div>

                    <div class="form-under">
                        <RememberButton @onRemember="onRemember"/>
                        <div class="forgotPassword-wrapper">
                            <a href="#">Забыли пароль?</a>
                        </div>
                    </div>

                    <div v-if="error" class="errors">{{error}}</div>
                    <LoginButton @click="submitHandler"/>
                    <div class="form-no-account">
                        <span>Нет аккаунта?</span>
                        <a href="#">Зарегистрироваться</a>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<script lang="ts">
import {Vue, Component, Watch} from 'vue-property-decorator';
import RememberButton from '@/components/RememberButton.vue';
import LoginButton from '@/components/LoginButton.vue';

@Component({
    components: {
        RememberButton,
        LoginButton
    }
})
export default class ArticlesComponent extends Vue{
    private login: string = '';
    private password: string = '';
    private remember: boolean = false;
    private error: string = '';

    private passwordTemplate = /[^A-Z-a-z-0-9]/i; 

    submitHandler() {
        console.log(this.login.length, this.password.length);
        if (this.login.length === 0 || this.password.length === 0) {
            this.error = 'Заполните все поля';
        }else if (this.login.length < 6) {
             this.error = ' Слишком короткий логин';
        } else if (this.password.length < 8) {
            this.error = 'Минимальная длина пароля 8 символов';
        } else if (this.passwordTemplate.test(this.password) || this.passwordTemplate.test(this.login)) {
            this.error = 'Неразрешенные символы';
        } else {
            this.error = '';
            let result = {
                login: this.login,
                password: this.password,
                remmember: this.remember
            };
            console.log(result);
        }
        
    }

    onRemember(val: boolean) {
        this.remember = val;
        console.log(val);
    }
}   
</script>

<style lang="scss" scoped>
    #login-page {
        position: absolute;
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;

        form {
            width: 933px;
            height: 649px;
            border-radius: 20px;
            position: relative;
            font-family: Inter;
            font-style: normal;

            .left {
                position: absolute;
                width: 489px;
                height: 100%;
                left: 0;
                display: flex;
                justify-content: center;
                align-items: center;
                z-index: 4;

                img{
                    position: absolute;
                    z-index: 0;
                }
                .blackout{
                    position: absolute;
                    width: inherit;
                    height: inherit;

                    z-index: 1;
                    background: rgba(0, 117, 255, 0.85);
                    border-radius: 20px 0px 0px 20px;
                }
                .left-text{
                    position: absolute;
                    color: white;
                    z-index: 3;
                    text-align: left;

                    top: 208px;
                    left: 92px;

                    .title{
                        font-weight: bold;
                        font-size: 54px;
                        line-height: 65px;
                        margin: 0;
                        margin-bottom: 16px;
                    }

                    .description{
                        margin: 0;
                        font-weight: 500;
                        font-size: 16px;
                        line-height: 19px;
                    }
                }
            }
            .right {
                position: absolute;
                height: 100%;
                width: 500px;
                right: 0;
                z-index: 5;
                background: #fff;
                border-radius: 20px;

                display: flex;
                justify-content: center;
                align-items: center;

                .content{
                    // background: #000;
                    width: 295px;
                    height: 462px;
                    font-weight: 500;

                    .form-title{
                        font-size: 24px;
                        line-height: 29px;
                        margin: 0;
                        margin-bottom: 24px;
                    }
                    .form-description{
                        font-size: 16px;
                        line-height: 19px;

                        color: #AAAAAA;
                    }

                    .form-inputs{
                        margin-top: 61px;

                        input {
                            border: none;
                            border-bottom: 2px solid;
                            border-color: #DEDEDE;
                            outline: none;

                            cursor: pointer;

                            background-repeat: no-repeat;
                            padding-left: 26px;

                            width: calc(295px - 26px);
                            height: 36px;

                            font-size: 18px;
                            line-height: 22px;
                            // color: #595959;
                            transition: all .03s linear;

                            margin-bottom: 25px;

                            &::placeholder {
                                font-size: 18px;
                                line-height: 22px;
                                color: #595959;
                                transition: color .03s linear;
                            }

                            &:focus{
                                border-color: #0075FF;

                                &::placeholder {
                                    color: #0075FF;
                                }
                            }
                        }
                        
                        input {
                            &#login{
                                background-position: 0 8px;
                                background-size: 18px;
                                background-image: url('../assets/images/login_icon.svg');
                            }
                            &#password{
                                background-position: 0 8px;
                                background-size: 13px 18px;
                                margin-bottom: 35px;
                                background-image: url('../assets/images/password_icon.svg');
                            }

                            &:focus {
                                &#login{
                                    background-image: url('../assets/images/login_icon-active.svg');
                                }
                                &#password{
                                    background-image: url('../assets/images/password_icon-active.svg');
                                }
                            }
                        }
                    }

                    .form-under{
                        display: flex;
                        justify-content: space-between;

                        .forgotPassword-wrapper{
                            a {
                                text-decoration: none;
                                color: #AAAAAA;
                                transition: color .04s linear;

                                &:hover {
                                    color: #0075FF;
                                }
                            }
                        }

                    }

                    .errors{
                        color: rgb(231, 60, 60);
                        position: absolute;
                        width: 295px;
                        text-align: center;
                        margin-top: 10px;
                    }

                    .form-no-account{
                        width: 295px;
                        display: flex;
                        justify-content: center;

                        * {
                            font-size: 16px;
                            line-height: 19px;
                            color: #AAAAAA;
                            margin-right: 7px;
                        }

                        a {
                            text-decoration: none;
                            color: #0075FF;
                        }
                    }
                }
            }
        }
    }
</style>