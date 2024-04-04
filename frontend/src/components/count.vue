<template>
    <div class="gradient-custom">
        <h2>Som coin: {{ count }}</h2>
        <img class="coin" @click="CountInc" src="../../public/img/icons/sticker.webp" alt="somcoin">
    </div>
</template>
<script>
export default {
    data() {
        return {
            count: localStorage.getItem('count'),
        }
    },
    methods:{
        CountInc(){
            this.count ++
            localStorage.setItem('count', this.count)
        }
    },
}
</script>
<style scoped>
    .gradient-custom{
        width: 100%;
        height: 90vh;
        background-image: linear-gradient(-20deg, #ff2846 0%, #6944ff 100%);
        padding-top:100px;
        padding-bottom:100px;
    }

    .coin{
        width:150px;
        border:none;
        border-radius:50%;
        color:#fff;
        background:#2c3e50;
    }
</style>