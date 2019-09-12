<template>
    <div>
        <firstpage v-if="page === 1"></firstpage>
        <secondpage v-else-if="page === 2"></secondpage>
    </div>
</template>

<script>
import firstpage from './components/firstPage'
import secondpage from './components/secondPage';
export default {
    data: function(){
        return {
            page: 1
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