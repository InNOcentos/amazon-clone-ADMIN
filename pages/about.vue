<template>
    <div>
        <h1>{{name}}</h1>
        
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name: 'test'
            }
        },
        methods: {
            onClick() {
                alert('i am here')
            }
        }
    }
</script>

<style>


</style>