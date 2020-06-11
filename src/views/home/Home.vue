/* eslint-disable */
<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <HomeSwiper :banners="banners"></HomeSwiper>
    <RecommendView :recommends="recommends"></RecommendView>
  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  import HomeSwiper from "./childComs/HomeSwiper";
  import RecommendView from "./childComs/RecommendView";
  import {getHomeMultidata} from "network/home";

  export default {
    name: "Home",
    data() {
      return{
          banners:[],
          recommends:[]
      }
    },
    components:{
      NavBar,
      HomeSwiper,
      RecommendView
    },
    created() {
      //1.请求多个数据
      getHomeMultidata().then(res => {
          this.banners = res.data.data.banner.list;
          this.recommends = res.data.data.recommend.list;
      }).catch()
    }
  }
</script>

<style scoped>
  .home-nav{
    background-color: var(--color-tint);
    color: #fff;
  }
</style>
