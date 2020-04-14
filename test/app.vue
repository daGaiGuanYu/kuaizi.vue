<template lang="pug">
  .root-root
    .upper
      span 这是 collapse-box 上面的东西
      span.btn(@click="collapse=!collapse") {{collapse?'放':'收'}}
    collapse-box(:collapse="collapse") haha
    .underneath 这是 collapse-box 下面的东西
</template>

<script>
import CollapseBox from '../src/index.vue'

export default {
  name: 'root-root',
  components: {
    CollapseBox
  },
  data(){
    return {
      collapse: false
    }
  }
}
</script>

<style lang="stylus">
body
  line-height: 36px
.btn
  display: inline-block
  width: 36px
  text-align: center
  margin: 10px
  background: #000
  color: #fff
  border-radius: 18px
  user-select: none
  cursor: pointer
</style>