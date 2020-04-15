# collapse-box.vue
一个简陋的 Vue 组件，用来呈现高度的塌陷效果
[!]()

## 开始
##### 安装
``` bash
npm install collapse-box.vue
```

##### 使用
``` vue
<template>
  <div class="root-el" @click="collapse=!collapse">
    <div class="upper">这是 collapse-box 上面的东西</div>
    <collapse-box :collapse="collapse">
      <div>haha</div>
      <div>heihei</div>
      <div>gogo</div>
    <div class="underneath">这是 collapse-box 下面的东西</div>
  </div>
</template>

<script>
import CollapseBox from 'collapse-box.vue' // .vue 不能省略

export default {
  name: 'root-root',
  components: {
    CollapseBox // 注册组件
  },
  data(){
    return {
      collapse: false // 控制 collapse-box 的收放
    }
  }
}
</script>
```

## 注意事项
+ 建议读一读源码（很少）
+ 不要在 collapse-box 的根元素上添加样式，除非你读了源码
+ 元素塌陷时，只是把高度设置成为了 0px
+ 源码真的很少，至少应该扫一眼
