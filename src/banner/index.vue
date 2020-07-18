<template lang="pug">
  .kuaizi-banner
    .list(ref="list")
      slot
    .dot-list
      .dot(v-for="index in sum" @mouseover="setCurrent(index-1)" :class="{ selected: index-1 == realCurrent }")
</template>

<script>
export default {
  name: 'banner',
  props: {
    animationDuration: {
      type: Number,
      default: 300
    },
    intervalDuration: {
      type: Number,
      default: 3000
    },
    autoplay: Boolean, // 是否自动播放
    current: Number, // 当前展示哪一个
  },
  data(){
    return {
      realCurrent: 0,
      sum: 0
    }
  },
  watch: {
    current(nv){
      this.setCurrent(nv)
    }
  },
  methods: {
    init(){ // children 变动时，外部调用
      const children = this.$refs.list.children
      this.sum = children.length

      const duration = this.animationDuration/1000
      for(let dom of children)
        dom.style.transition = 'all ' + duration + 's'

      const interval = this.intervalDuration + this.animationDuration
      if(this.autoplay && this.sum>1)
        setInterval( () => this.next() , interval)
      
      const cDom = children[0]
      cDom.style.display = 'block'
      cDom.style.left = 0
    },
    next(){
      const children = this.$refs.list.children
      initAllDom(children)

      const ov = this.realCurrent
      let nv = ov + 1
      if(nv == this.sum)
        nv = 0
      this.realCurrent = nv

      // 自动播放，均是左到右
      leave2Left(children[ov])
      enterFromRight(children[nv])
    },
    setCurrent(nv){
      const ov = this.realCurrent
      if(ov == nv) return 
      this.realCurrent = nv

      const children = this.$refs.list.children
      initAllDom(children)

      if(ov<nv){ // 新的在右边
        leave2Left(children[ov])
        enterFromRight(children[nv])
      }else{
        leave2Right(children[ov])
        enterFromLeft(children[nv])
      }
    }
  },
  mounted(){
    this.init()
  }
}

// 初始化所有 dom
function initAllDom(list){
  for(let dom of list)
    dom.style.display = '' // css 里有 none
}
// 左边进入
function enterFromLeft(dom){
  dom.style.left = '-100%'
  requestAnimationFrame( () => {
    dom.style.display = 'block'
    requestAnimationFrame( () => {
      dom.style.left = '0'
    })
  })
}
// 左边出
function leave2Left(dom){
  dom.style.display = 'block'
  dom.style.left = '-100%'
}
// 右边进入
function enterFromRight(dom){
  dom.style.left = '100%'
  requestAnimationFrame( () => {
    dom.style.display = 'block'
    requestAnimationFrame( () => {
      dom.style.left = '0'
    })
  })
}
// 右边出
function leave2Right(dom){
  dom.style.display = 'block'
  dom.style.left = '100%'
}
</script>

<style lang="stylus" scoped>
.kuaizi-banner
  overflow: hidden
  position: relative
  height: auto
.list
  width: 100%
  height: 100%
.dot-list
  position: absolute
  left: 50%
  transform: translate(-50%, 0)
  bottom: 10%
.dot
  display: inline-block
  margin: 0 10px
  width: 10px
  height: 10px
  border-radius: 50%
  background: rgba(0, 0, 0, 0.5)
.selected
  background: rgba(0, 0, 0, 0.2)
</style>

<style lang="stylus">
.list > *
  width: 100%
  display: none
  position: absolute
</style>