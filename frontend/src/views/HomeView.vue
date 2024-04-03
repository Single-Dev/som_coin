<template>
  <div class="home">
   <Count/>
   <p>Som coin siteda hali coin toplash boshlanmadi. Shuning uchun xatoliklar kuzatilishi mumkin. Keltirilgan noqulayliklar uchun uzr so'raymiz!</p>
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
