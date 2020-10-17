<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <swiper>
      <swiper-item v-for="item in banners" :key="item">
        <a :href="item.link">
          <img :src="item.image" alt="">
        </a>
      </swiper-item>
    </swiper>
  </div>
</template>

<script>

  import NavBar from 'components/common/navbar/NavBar'
  import {getHomeMultidata} from 'network/home'
  import {Swiper,SwiperItem} from 'components/common/swiper'

export default {
  name: 'Home',
  data() {
    return {
      banners:[],
      recommends:[]
    }
  },
  components:{
    NavBar,
    Swiper,
    SwiperItem
  },
  created() {
    //1. 请求多个数据
    getHomeMultidata().then(res=>{
      this.banners = res.data.banner
      console.log(this.banners)
      this.recommends = res.data.recommend
    })
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .home-nav{
    background-color: var(--color-tint);
    color: white;
  }
</style>
