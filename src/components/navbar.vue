<template>
    <div class="navbar">
        
            <div class="left">
                <div class="box">
                    <a href="" @click.prevent="fetchimage"><i class="fas fa-toilet fa-2x"></i></a>
                </div>
                
            </div>
            <div class="right">
                <div class="box">
                    <a @click.prevent="favoriteimage" href="" >Your likes.</a>
                </div>
                <div class="box">
                    <a @click.prevent="signout" href="">Sign out.</a>
                </div>
            </div>
     
    </div>
</template>

<script>
export default {
    data: function(){
        return {

        }
    },
    methods: {
        signout(){
            localStorage.removeItem('')
            this.$emit('logout')
        },
        fetchimage(){
            this.$emit('fetchimage')
        },
        favoriteimage(){
            this.$emit('favoriteimage')
        }
    }
}
</script>

<style scoped>
    .box{
        height: 100%;
        display: flex;
        align-items: center;

    }
    .left .box{
        padding-left: 3vw;
    }
    .right .box {
        padding-right: 3vw;
    }
    .right {
        display: flex;
        flex-direction: right;
    }
    .navbar a:hover {
        border-bottom: 2px solid black;
        
    }
    .navbar a {
        color: black;
        text-decoration: none;
    }
    .navbar {
        font-family: 'Roboto', sans-serif;
        height: 6vh;
        display: flex;
        color: black;
        justify-content: space-between;
    }
</style>