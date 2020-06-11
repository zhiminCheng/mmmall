/* eslint-disable */
<template>
  <div id="home">
    <NavBar class="home-nav">
      <div slot="center">购物街</div>
    </NavBar>
    <HomeSwiper :banners="banners"></HomeSwiper>
    <RecommendView :recommends="recommends"></RecommendView>
    <feature-view></feature-view>
  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  import HomeSwiper from "./childComs/HomeSwiper";
  import RecommendView from "./childComs/RecommendView";
  import FeatureView from "./childComs/FeatureView";
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
      RecommendView,
      FeatureView
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
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9;
  }
</style>
