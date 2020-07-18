<template lang="pug">
  .demo
    h1 banner
    banner(:autoplay="true")
      .item 1111111111111111111111111
      .item 2222222222222222222222222
      .item 3333333333333333333333333
</template>

<script>
import Banner from '../../src/banner/index.vue'

export default {
  name: 'banner-demo',
  components: {
    Banner
  },
  data(){
    return {
      collapse: false
    }
  }
}
</script>

<style lang="stylus" scoped>
.kuaizi-banner
  width: 300px
  height: 200px
</style>