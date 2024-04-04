<template>
  <div class="home">
   <Count/>
  </div>
</template>

<script>
// @ is an alias to /src
import Count from '@/components/count.vue'

export default {
  name: 'HomeView',
  components: {
    Count
  }
}
</script>

<style scoped>
  p{
    width: 200px;
    margin-left: auto;
    margin-right: auto;
  }
</style>
