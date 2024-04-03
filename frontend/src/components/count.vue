<template>
    <div>
        <h2>Balansingiz: {{ count }}</h2>
        <button @click="CountInc">Tap</button>
    </div>
</template>
<script>
export default {
    data() {
        return {
            count: 0,
        }
    },
    methods:{
        CountInc(){
            this.count ++
            localStorage.setItem('count', this.count)
        }
    }
}
</script>
<style lang="">
    
</style>