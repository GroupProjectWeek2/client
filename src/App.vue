<template>
    <div>
        <h1>{{test}}</h1>
        <login @tambaho="tambahO"></login>
    <div>
</template>

<script>

export default {
    data: function(){
        return {
            test: "halooo"
        }
    },
    methods: {
        tambahO(){
            this.test+= 'o'
        }
    },
    components : {
        login : loginForm
    }
}
</script>

<style>
    h1 {
        color: red;
    }
</style>