<template>
  <div class="discovery-container">
    <!-- 轮播图 -->
    <el-carousel class="" :interval="4000" type="card">
<!--      //循环获取到的接口数据-->
      <el-carousel-item v-for="(item,index) in banners" :key="index" >
        <img :src="item.imageUrl" alt="" />
      </el-carousel-item>
    </el-carousel>
    <!-- 推荐歌单 -->
    <div class="recommend">
      <h3 class="title">
        推荐歌单
      </h3>
      <div class="items" v-for="(item,index) in list" :key="index"   @click="toPlaylist(item.id)">
        <div class="item">
          <div class="img-wrap">
            <div class="desc-wrap">
              <span class="desc">{{item.copywriter}}</span>
            </div>
            <img :src="item.picUrl" alt="" />
            <span class="iconfont icon-play"></span>
          </div>
          <p class="name">{{item.name}}</p>
        </div>
      </div>
    </div>
    <!-- 最新音乐 -->
    <div class="news">
      <h3 class="title">
        最新音乐
      </h3>
      <div class="items">
        <div class="item" v-for="(item,index) in songs" :key="index">
          <div class="img-wrap">
            <img :src="item.picUrl" alt="" />
            <span @click="playMusic(item.id)" class="iconfont icon-play"></span>
          </div>
          <div class="song-wrap">
            <div class="song-name">{{item.name}}</div>
            <div class="singer">{{item.artistName}}</div>
          </div>
        </div>
      </div>
    </div>
    <!-- 推荐MV -->
    <div class="mvs">
      <h3 class="title">推荐MV</h3>
      <div class="items">
        <div class="item" v-for="(item,index) in mvs" :key="index" @click="toMV(item.id)" >
          <div class="img-wrap">
            <img :src="item.picUrl" alt="" />
            <span class="iconfont icon-play"></span>
            <div class="num-wrap">
              <div class="iconfont icon-play"></div>
<!--              //播放次数-->
              <div class="num">{{item.playCount}}</div>
            </div>
          </div>
          <div class="info-wrap">
<!--            //mv名-->
            <div class="name">{{item.name}}</div>
<!--            //歌手-->
            <div class="singer">{{item.artistName}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'discovery',
  data(){
    return{
      //轮播图
      banners:[],
      //推荐歌单
      list:[],
    //最新音乐
      songs:[],
      //MV
      mvs:[]
    }
  },
  created() {
    //轮播图接口
    axios({
      url:'https://autumnfish.cn/banner',
      method:'get',
    }).then(res => {
      // console.log(res.data.banners)
      this.banners = res.data.banners
    }),
    //推荐歌单
    axios({
      url:' https://autumnfish.cn/personalized',
      method:'get',
      params:{
        //获取的数据量
        limit:10
      }
    }).then(res => {
      // console.log(res.data.result)
      this.list = res.data.result
    }),
            //最新音乐
            axios({
              url:' https://autumnfish.cn/personalized/newsong',
              method:'get',
              params:{
                //获取的数据量
                limit:10
              }
            }).then(res => {
              // console.log(res)
              this.songs = res.data.result
            }),
            //推荐mv
            axios({
              url:' https://autumnfish.cn/personalized/mv',
              method:'get',
              // params:{
              //   //获取的数据量
              //   limit:10
              // }
            }).then(res => {
              console.log(res.data.result)
              this.mvs = res.data.result
            })

  },
  methods:{
      toPlaylist(id){
          //跳转并携带数据 两种方法
          // this.$router.push('/playlist?q='+id)
          this.$router.push(`/playlist?q=${id}`)
      },
      //跳转MV页面
      toMV(id){
          this.$router.push(`/mv?q=${id}`)
      },
    playMusic(id){
      axios({
        url:' https://autumnfish.cn/song/url',
        method:'get',
        params:{
          id
        }
      }).then(res => {

        let url = res.data.data[0].url
          console.log(res.data.data[0])
          console.log(res.data.data[0].url)
          console.log(this.$parent.musicUrl)
          // //设置给父组件的播放地址
          this.$parent.musicUrl = url
        // this.$parent.musicUrl = res.data[0].url
      })
    }
  }
};
</script>

<style >
.discovery-container .recommend .items{
  display: inline-block;
}

</style>
