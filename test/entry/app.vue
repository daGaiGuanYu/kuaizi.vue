<template lang="pug">
  .root-root
    collapse-box-demo
</template>

<script>
import CollapseBoxDemo from '../cmp/collapse-box'

export default {
  components: {
    CollapseBoxDemo
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