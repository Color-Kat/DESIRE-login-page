<template>
     <div class="remember-wrapper">
        <input 
            type="checkbox" 
            name="rememver" 
            id="remember"
            v-model="remember"
            class="custom-checkbox"
            :checked="remember"
        >
        <label for="rememver" @click="rememberClick"><span>Запомнить</span></label>
    </div>
</template>

<script lang="ts">
import {Vue, Component,} from 'vue-property-decorator';

@Component
export default class RememberButton extends Vue{
    private remember: boolean = false;

    rememberClick() {
        this.remember = !this.remember;
        this.$emit('onRemember', this.remember)
    }
}   
</script>


<style lang="scss" scoped>
    .remember-wrapper {
        height: 19px;
        display: flex;
        align-items: center;
        position: relative;

        user-select: none;

        #remember {
            position: absolute;
            z-index: 10;
            opacity: 0;
            z-index: 1;
        }

        .custom-checkbox+label {
            display: inline-flex;
            align-items: center;
            user-select: none;
        }
        label {
            transition:  all .1s linear;
            cursor: pointer;
            z-index: 2;

            &:hover {
                span{
                    color: #0075FF;
                }

                &:hover{
                     &:before, &+input{
                        border-color: #0075FF;
                    }
                }
            }
        }

        // label:hover {
        //     // &: {
        //         &:before, &+input{
        //             border-color: #0075FF;
        //         }
        //     // }
            
        // }
        // label:hover span{
        //     color: #0075FF;
        // }

        // input:hover+label:before { border-color: #0075FF;}
        .custom-checkbox+label::before {
            content: '';
            display: inline-block;
            width: 19px;
            height: 19px;

            flex-shrink: 0;
            flex-grow: 0;

            border: 2px solid;
            border-color: #AAAAAA;
            box-sizing: border-box;
            border-radius: 4px;
            margin-right: 10px;

            background-repeat: no-repeat;
            background-position: center center;
            background-size: 50% 50%;
            transition:  all .01s linear;
        }

        .custom-checkbox:checked+label::before {
            border-color: #0075FF;
            background-color: #0075FF;
            background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
        }
        // .custom-checkbox:not(:disabled):not(:checked)+label:hover::before {
        //     border-color: #0075FF;
        // }
    }
</style>