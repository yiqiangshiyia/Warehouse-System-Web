<template>
  <div id="app">
     <router-view/>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {},
  //解决前端刷新页面路由丢失问题
  data(){
    return{
      user : JSON.parse(sessionStorage.getItem('CurUser'))
    }
  },
  watch:{
    '$store.state.menu':{
      handler(val,old){
        console.log(val)
        if(!old && this.user && this.user.no){
          this.$store.commit('setMenu',val)
        }
      },
      immediate: true
    }
  }
}
</script>

<style>
#app {
    height: 100%;
}
</style>


<!--
  前端学习笔记01：
  App.vue是什么：App.vue是项目的主组件，页面入口文件 ，所有页面都在App.vue下进行切换，
  app.vue负责构建定义及页面组件归集。
  App.vue本质上也是一个js文件，相当于一个模板文件（描述一个组件）。
  主要包括三个部分模板（结构）、脚本文件、样式
    模板（结构）：<template></template> template内容相当于MVVM中的V——视图层
    脚本文件 ： <script></script> script标签内容相当于MVVM中的VM——数据绑定交互
    样式文件 ： <style></style>
  App.vue作用：1.app.vue作为主组件在main.js中被使用
              2.主组件app.vue调用其他组件，构建页面
-->

<!--
  前端学习笔记03：
  <router-view/>作用：Vue路由中的<router-view/>是用来承载当前级别下的子级路由的一个视图标签，
  此标签的作用就是显示当前路由级别下一级的页面。
-->