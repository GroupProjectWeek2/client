<template>
    <div>
<<<<<<< HEAD
        <h1>{{test}}</h1>
        <login @tambaho="tambahO"></login>
    <div>
</template>

<script>

=======
        <firstpage v-if="page === 1"></firstpage>
        <secondpage v-else-if="page === 2"></secondpage>
    </div>
</template>

<script>
import firstpage from './components/firstPage'
import secondpage from './components/secondPage';
>>>>>>> testvue
export default {
    data: function(){
        return {
            page: 1
        }
    },
<<<<<<< HEAD
    methods: {
        tambahO(){
            this.test+= 'o'
        }
    },
    components : {
        login : loginForm
=======
    components: {
        firstpage,
        secondpage
>>>>>>> testvue
    }

}
</script>

<style>
<<<<<<< HEAD
    h1 {
        color: red;
    }
=======
    
>>>>>>> testvue
</style>