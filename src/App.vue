<template>
    <div>
        <firstpage  @fetchimage="fetchImages" v-if="page === 1"></firstpage>
        <secondpage @registerimage="registerimage" @likethis="likethis" @favoriteimage="favoriteimage" @searchimage="searchImage" @fetchimage="fetchImages" @logout="logout" :images="images" v-else-if="page === 2"></secondpage>
    </div>
</template>

<script>
import firstpage from './components/firstPage'
import secondpage from './components/secondPage';
import axios from 'axios'
export default {
    data: function(){
        return {
            page: 1,
            images: [],
            baseUrl: "http://34.87.72.235",
        }
    },
    methods: {
        favoriteimage(){
            // axios({
            //         url: `${this.baseUrl}/images`,
            //         method: 'get',
            //         headers: {
            //             token: localStorage.getItem('token')
            //         }
            // })
            // .then(response => {
            //     this.images = response.data
            //     this.page = 2
            // })
            // .catch(err => {
            //     if(err.response){
            //         this.error = err.response.data.message
            //     }else if(err.request){
            //         this.errorMessage = `500 Internal Server Error`
            //     }else {
            //         console.log(err.message)
            //     }
            // })
        },
        registerimage(value){

            console.log(value)
        },
        likethis(_id){
            axios({
                    url: `${this.baseUrl}/images/favorites/${_id}`,
                    method: 'post',
                    headers: {
                        token: localStorage.getItem('token')
                    }
            })
            .then(response => {
                alert('sukses like')
                this.fetchImages()
                
            })
            .catch(err => {
                if(err.response){
                    this.error = err.response.data.message
                }else if(err.request){
                    this.errorMessage = `500 Internal Server Error`
                }else {
                    console.log(err.message)
                }
            })
        },
        logout(){
            localStorage.removeItem('token')
            this.page = 1;
        },
        setimages(page, event){
            this.images = event
            this.page = page
        },
        fetchImages(){
            axios({
                    url: `${this.baseUrl}/images`,
                    method: 'get',
                    headers: {
                        token: localStorage.getItem('token')
                    }
            })
            .then(response => {
                this.images = response.data
                this.page = 2
                console.log(this.images)
            })
            .catch(err => {
                if(err.response){
                    this.error = err.response.data.message
                }else if(err.request){
                    this.errorMessage = `500 Internal Server Error`
                }else {
                    console.log(err.message)
                }
            })
        },
        searchImage(tag){
            axios({
                url: `${this.baseUrl}/images/search/${tag}`,
                method: 'get',
                headers: {
                token: localStorage.getItem('token')
            }
            })
            .then(response => {
                this.images = response.data
            })
            .catch(err => {
                if(err.response){
                    this.error = err.response.data.message
                }else if(err.request){
                    this.errorMessage = `500 Internal Server Error`
                }else {
                    console.log(err.message)
                }
            })
        }
    },
    components: {
        firstpage,
        secondpage
    }

}
</script>

<style>
    
</style>