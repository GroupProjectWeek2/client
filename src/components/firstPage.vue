<template>
    <div id="loginform">
        <loginform @fetchimage="fetchimage"></loginform>
    </div>
</template>

<script>
import loginform from './loginFrom'
export default {
    data: function(){
        return {
        }
    },
    methods: {
        fetchimage(){
            
            this.$emit('fetchimage')
        }
    },
    components: {
        loginform
    }
}
</script>

<style>
    #loginform {
        display: flex;
        height: 100vh;
        width: 100vw;
        justify-content: center;
        align-items: center;
    }
</style>