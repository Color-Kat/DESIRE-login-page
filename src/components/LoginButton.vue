<template>
    <button class="form-button" type="submit">{{message}}</button>
</template>

<script lang="ts">
import {Vue, Component, Prop} from 'vue-property-decorator';

@Component
export default class LoginButton extends Vue{
    @Prop({ default: 'Войти' }) readonly message!: string 
}   
</script>

<style lang="scss" scoped>
     .form-button{
        margin-top: 60px;
        margin-bottom: 28px;
        width: 295px;
        height: 41px;

        border-radius: 83px;
        border: none;

        background: #0075FF;
        transition: background .08s linear;
        color: #fff;
        outline: none;

        font-size: 18px;
        line-height: 22px;
        cursor: pointer;
        
        &:hover{
            background: rgb(22, 131, 255);
        }
    }
</style>