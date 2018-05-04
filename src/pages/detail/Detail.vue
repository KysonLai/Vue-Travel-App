<template>
  <div>
    <detail-banner :sightName="sightName" :bannerImg="bannerImg" :bannerImgs="gallaryImgs"></detail-banner>
    <detail-header></detail-header>
    <div class="container">
      <detail-list :list="list"></detail-list>
    </div>
  </div>
</template>

<script>
  import DetailBanner from "./components/Banner.vue";
  import DetailHeader from "./components/Header.vue";
  import DetailList from "./components/List.vue";
  import axios from 'axios'
  export default {
    name: 'Detail',
    components:{
      DetailBanner,
      DetailHeader,
      DetailList,
    },
    data (){
      return{
        sightName:'',
        bannerImg:'',
        gallaryImgs:[],
        list:[]
      }
    },
    methods:{
      getDetailInfo (){
          axios.get('/static/mock/detail.json',{
            params:{
              id:this.$route.params.id
            }
          })
            .then(this.handelGetDataSucc)
      },
      handelGetDataSucc (res){
        res = res.data;
        if(res.ret && res.data){
          const data = res.data
          this.sightName = data.sightName
          this.bannerImg = data.bannerImg
          this.gallaryImgs = data.gallaryImgs
          this.list = data.categoryList
        }
      }
    },
    mounted (){
      this.getDetailInfo()
    }
  }
</script>

<style lang="stylus" scoped>
  .container
    height :50rem
</style>
