<template lang="pug">
  .demo
    h1 collapse-box
    .upper
      span 这是 collapse-box 上面的东西
      span.btn(@click="collapse=!collapse") {{collapse?'放':'收'}}
      
      collapse-box(:collapse="collapse")
        .haha haha
        .heihei heihei
      
      .underneath 这是 collapse-box 下面的东西
</template>
<script>
import CollapseBox from '../../src/collapse-box/index.vue'

export default {
  name: 'collapse-box-demo',
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