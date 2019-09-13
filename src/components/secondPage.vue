<template>
    <div>
        <navbar @favoriteimage="favoriteimage" @fetchimage="fetchimage" @logout="logout" style="margin-bottom: 10vh;"></navbar>
        <contentsecondpage @registerimage="registerimage" @likethis="likethis" @searchimage="searchimage" :images="images"></contentsecondpage>
    </div>
</template>

<script>
import contentsecondpage from './secondPageContent'
import navbar from'./navbar'
export default {
    props:['images'],
    data: function(){
        return {

        }
    },
    methods: {
        registerimage(value){
            this.$emit('registerimage', value)
        },
        likethis(_id){
            this.$emit('likethis', _id)
        },
        favoriteimage(){
            this.$emit('favoriteimage')
        },
        logout(){
            this.$emit('logout')
        },
        fetchimage(){
            this.$emit('fetchimage')
        },
        searchimage(value){
            this.$emit('searchimage', value)
        }
    },
    components: {
        contentsecondpage,
        navbar
    }
}
</script>

<style>

</style>