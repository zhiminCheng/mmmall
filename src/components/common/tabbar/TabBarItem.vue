<template>
  <div class="tab-bar-item" @click="itemClick">
    <slot v-if="!isActive" name="item-icon"></slot>
    <slot v-else name="item-icon-active"></slot>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>

</template>

<script>
    export default {
        name: "TabBarItem",
        props:{
            path:String,
            activeColor:{
                type:String,
                default:"red"
            }
        },
        data(){
            return {

            }
        },
        computed:{
            isActive(){
                return this.$route.path.indexOf(this.path) !== -1;
            },
            activeStyle(){
                return this.isActive ? {color:this.activeColor} : {};
            }
        },
        methods:{
            itemClick(){
                this.$router.replace(this.path);
            }
        }
    }
</script>
<!--vue-router.esm.js?fe87:2007 Uncaught (in promise) NavigationDuplicated {_name: "NavigationDuplicated", name: "NavigationDuplicated"}
路由报错 两种解决方法



解决方法一：经过多次尝试发现原因可能是 在重新下载依赖包时，安装的vue-router还是之前出错的那个版本，

解决方法也很简单，在项目目录下运行 npm i vue-router@3.0 -S 即可。

解决方法二：如果你不想用方法一那就在 main.js里添加一段代码。



import Router from 'vue-router'
const routerPush = Router.prototype.push
Router.prototype.push = function push(location) {
return routerPush.call(this, location).catch(error=> error)
}-->
<style scoped>
  #tab-bar .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
  #tab-bar .tab-bar-item:hover .inactivedIcon{
    display: none;
  }
  #tab-bar .tab-bar-item .activedIcon{
    display: none;
  }
  #tab-bar .tab-bar-item:hover .activedIcon{
    display: block;
  }
  #tab-bar .tab-bar-item img{
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
  }
</style>
