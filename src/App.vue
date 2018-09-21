<template>
  <div id="app">
    <app-header :poiInfo="poiInfo"></app-header>
    <!-- 导航 -->
    <app-nav :commentNum="commentNum"></app-nav>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
  </div>
</template>

<script>
import Header from './components/header/Header'
import Nav from './components/nav/Nav'
export default {
  name: 'App',
  components:{
    "app-header":Header,
    "app-nav":Nav
  },
  data(){
    return {
      poiInfo:{

      },
      commentNum:0
    }
  },
  created(){
    fetch("/api/goods").then(res =>{
      return res.json()
    }).then(response =>{
      if(response.code==0){
        this.poiInfo = response.data.poi_info;
      }
      //console.log(response)
    })
    fetch("/api/ratings").then(res =>{
      return res.json()
    }).then(response =>{
      if(response.code==0){
        this.commentNum = response.data.comment_num;
      }
      //console.log(response)
    })
  }
}
</script>

<style>

</style>
