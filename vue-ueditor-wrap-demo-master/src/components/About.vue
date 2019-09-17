<template>
  <div>
    <p align="center"><img src="../assets/logo.png" alt="logo"></p>
    <p align="center">这是一个使用 <b>vue-ueditor-wrap</b> 的 Vue 项目。</p>
     <div class="hello">
    <div @click="showData" class="preview" v-html="msg"></div>
    <!-- 你不需要担心一个页面中过多vue-ueditor-wrap组件会导致混乱,或者重复引用JS(打开控制台瞄一眼),每个组件都保证拥有一个独立的UEditor实例,你可以尝试把数字改成99(根据自己电脑自行斟酌),但依然稳定可用 -->
    <vue-ueditor-wrap ref="ueditor" v-model="msg" :destroy="false" :config="config" @ready="ready" ></vue-ueditor-wrap>
  </div>
  </div>
</template>
<script>
// 1、引入VueUeditorWrap组件
import VueUeditorWrap from 'vue-ueditor-wrap' // ES6 Module
// const VueUeditorWrap = require('vue-ueditor-wrap') // CommonJS
export default {
  name: 'HelloWorld',
  // 2、注册组件
  components: {
    VueUeditorWrap
  },
  data () {
    return {
      // 3、v-model绑定数据
      msg: '<h2>1</h2>',
      // 4、根据项目需求自行配置,具体配置参见ueditor.config.js源码或 http://fex.baidu.com/ueditor/#start-start
      config: {
        // 编辑器不自动被内容撑高
        autoHeightEnabled: false,
        // 初始容器高度
        initialFrameHeight: 240,
        // 初始容器宽度
        initialFrameWidth: '100%',

          serverUrl: 'https://www.ishangmi.cn/ueditor/config'

      }
    }
  },
  mounted () {
    console.log('%c注意：本Demo提供的serverUrl是为了方便小伙伴们体验图片文件等上传功能。\n请勿在生产环境使用此serverUrl！！！', 'background:#f33;color:#fff')
  },
  methods: {
    // 5、 你可以在ready方法中拿到editorInstance实例,所有API和官方的实例是一样了。http://fex.baidu.com/ueditor/#api-common
    ready (editorInstance) {
      console.log(`实例${editorInstance.key}已经初始化:`, editorInstance)
    },
    // 6. 查看绑定的数据
    showData () {
      alert(this.msg)
      console.log(this.msg)
    },
    // 7. 借助 beforeInit 钩子，你可以实现对 UEditor 的二次开发，会在 scripts 加载完毕之后、编辑器初始化之前触发，以 编辑器 id 和 配置参数 作为入参
   
  }
}
</script>

<style>
.preview{
  min-height: 150px;
}
</style>