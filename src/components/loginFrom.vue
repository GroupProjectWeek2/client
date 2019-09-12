<template>
    <form action="">
        <input v-model="email" type="email" placeholder="Email">
        <input v-model="password" type="password" placeholder="Password">
        <button @click.prevent="login" type="submit">Sign in</button>
    </form>
</template>

<script>
export default {
    data: function(){
        return {
            email: "",
            password: ""
        }
    },
    methods: {
        login(){
            console.log(this.email, this.password)
        }
    }
}
</script>

<style scoped>
    form{
        display: flex;
        flex-direction: column;
        width: 35vw;
    }
</style>