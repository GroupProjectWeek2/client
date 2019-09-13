<template>
    <div>
        <h1>Sign in.</h1>
        <div id="errorPosition">
            <p v-bind:style="{visibility: errorShow}">{{error}}</p>
        </div>
        <form action="">
            <input v-on:keyup.enter="login" v-model="email" type="email" placeholder="Email">
            <input v-on:keyup.enter="login" v-model="password" type="password" placeholder="Password">
            <button v-if="loading === false" @click.prevent="login" type="submit">Sign in</button>
            <button v-else type="submit"><i class="fas fa-spinner fa-pulse"></i></button>
            
        </form>
        <!-- <div class="g-signin2" data-onsuccess="onSignIn"></div> -->
        
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data: function(){
        return {
            email: "",
            password: "",
            error: "",
            errorShow: "hidden",
            loading: false,
            baseUrl: "http://34.87.72.235"
        }
    },
    methods: {
        login(){
            this.loading = true
            axios({
                method: 'post',
                url: `${this.baseUrl}/users/login`,
                data: {
                    email: this.email,
                    password: this.password
                }
            })
            .then(response =>{
                localStorage.setItem('token', response.data.token)
                this.loading = false
                this.errorShow = "hidden"
                this.errorMessage = ""
                this.email = ""
                this.password = ""
                this.$emit('fetchimage')

            })
            .catch(err => {
                this.loading = false
                
                if(err.response){
                    this.error = err.response.data.message
                }else if(err.request){
                    this.errorMessage = `500 Internal Server Error`
                }else {
                    console.log(err.message)
                }
                this.errorShow = "visible"
            })
        }
    }
}
</script>

<style scoped>
    #errorPosition{
        height: 8vh; 
        display:flex; 
        justify-items: start;
        align-items: flex-end;
        
    }
    form{
        display: flex;
        flex-direction: column;
    }
    p {
        font-family: 'Roboto', sans-serif;
        color: red;
        padding: 5px;
        position: relative;
        bottom: 0px;
        left: 0px;
        word-wrap:break-word;
        width: 100%;
        margin: 0px;
    }
    input, button{
        height: 5vh;
        box-sizing: border-box;
        border-radius: 5px;
        outline: none;
        border: 1px solid #cccccc;
        font-size: 1rem;
        margin-bottom: 1.5vh;
    }
    input {
        font-family: 'Roboto', sans-serif; 
        padding-left: 1vw;
    }
    button {
        background-color: black;
        color: white;
        font-size: 1.3rem;
        margin-top: 3vh;
        margin-bottom: 3vh;
        height: 6vh;
    }
    button:hover {
        background-color: #252625;
    }
    .g-signin2 {
        display: flex;
        justify-content: space-evenly;
    }
    div{
        font-family: 'Roboto', sans-serif; 
        width: 25vw;
    }
</style>


