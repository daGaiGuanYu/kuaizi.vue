<template>
  <div style="overflow-y: hidden" :style="{ height }">
    <slot />
  </div>
</template>

<script>
export default {
  props: ['collapse'],
  computed: {
    height(){
      return this.collapse?'0px':'auto'
    }
  },
  mounted(){

  }
}
</script>