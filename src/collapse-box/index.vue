<template>
  <div :style="{ 'overflow-y': 'hidden' }" ref="box">
    <slot />
  </div>
</template>

<script>
const defaultDuration = 300

export default {
  props: ['collapse', 'duration'],
  data(){
    return {
      _timeid: null
    }
  },
  computed: {
    d(){
      if(!this.duration)
        return defaultDuration
      
      let duration = parseInt(this.duration)
      
      if(isNaN(duration)){
        console.error('duration 属性应该是一个数字（单位为“毫秒”），已帮您替换为 300ms')
        return defaultDuration
      }
      return duration
    }
  },
  watch: {
    collapse(nv){
      if(this.$data._timeid)
        clearTimeout(this.$data._timeid)
      
      let box = this.$refs.box
      box.style.transition = ''
      
      let finalHeight
      if(nv){
        box.style.height = box.clientHeight + 'px'
        finalHeight = 0
      }else{
        box.style.height = ''
        finalHeight = box.clientHeight + 'px'
        box.style.height = 0

        setTimeout( () => { // 最后清除 height 限制
          box.style.height = ''
        }, this.d)
      }
      box.style.transition = `height ${this.d/1000}s` // 下次变化开始前去掉

      setTimeout( () => {
        box.style.height = finalHeight
      }, 50)
    }
  },
  mounted(){
    if(this.collapse)
      this.$refs.box.style.height = 0
  }
}
</script>