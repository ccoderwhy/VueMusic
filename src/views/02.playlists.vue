<template>
  <div class="playlists-container">
    <!-- 同步 -->
    <div class="top-card">
      <div class="icon-wrap">
<!--        封面-->
        <img :src="toplist.coverImgUrl" alt="" />
      </div>
      <div class="content-wrap">
        <div class="tag">精品歌单</div>
<!--        标题-->
        <div class="title">
          {{toplist.name}}
        </div>
<!--        介绍-->
        <div class="info">
          {{toplist.description}}
        </div>
      </div>
<!--      背景-->
      <img :src="toplist.coverImgUrl" alt="" class="bg" />
      <div class="bg-mask"></div>
    </div>
    <div class="tab-container">
      <!-- tab栏 顶部 -->
      <div class="tab-bar">
        <span class="item" :class="{active:tag=='全部'}" @click="tag='全部'">全部</span>
        <span class="item" :class="{active:tag=='欧美'}" @click="tag='欧美'">欧美</span>
        <span class="item" :class="{active:tag=='华语'}" @click="tag='华语'">华语</span>
        <span class="item" :class="{active:tag=='流行'}" @click="tag='流行'">流行</span>
        <span class="item" :class="{active:tag=='说唱'}" @click="tag='说唱'">说唱</span>
        <span class="item" :class="{active:tag=='摇滚'}" @click="tag='摇滚'">摇滚</span>
        <span class="item" :class="{active:tag=='民谣'}" @click="tag='民谣'">民谣</span>
        <span class="item" :class="{active:tag=='电子'}" @click="tag='电子'">电子</span>
        <span class="item" :class="{active:tag=='轻音乐'}" @click="tag='轻音乐'">轻音乐</span>
        <span class="item" :class="{active:tag=='影视原声'}" @click="tag='影视原声'">影视原声</span>
        <span class="item" :class="{active:tag=='ACG'}" @click="tag='ACG'">ACG</span>
        <span class="item" :class="{active:tag=='怀旧'}" @click="tag='怀旧'">怀旧</span>
        <span class="item" :class="{active:tag=='治愈'}" @click="tag='治愈'">治愈</span>
        <span class="item" :class="{active:tag=='旅行'}" @click="tag='旅行'">旅行</span>
      </div>
      <!-- tab的内容区域 -->
      <div class="tab-content">
        <div class="items">
          <div class="item" v-for="(item,index) in list" :key="index" @click="toPlaylist(item.id)">
            <div class="img-wrap">
              <div class="num-wrap">
                播放量:
                <span class="num">{{item.playCount}}</span>
              </div>
              <img :src="item.coverImgUrl" alt="" />
              <span class="iconfont icon-play"></span>
            </div>
            <p class="name">{{item.name}}</p>
          </div>
        </div>
      </div>
    </div>
    <!-- 分页器
    total总条数
    current-page当前页
    page-size每页多少条数据
    current-change页码改变事件
    -->
    <el-pagination
      @current-change="handleCurrentChange"
      background
      layout="prev, pager, next"
      :total="total"
      :current-page="page"
      :page-size="10"
    >
    </el-pagination>
  </div>
</template>

<script>
  import axios from 'axios'
export default {
  name: 'recommend',
  data() {
    return {
      // 总条数
      total:0,
      // 页码
      page:1,
      //顶部的推荐歌单
      toplist:{},
      //歌单列表
      list:[],
      //当前选择的数据
      tag:'全部'
    };
  },
  //侦听器
  watch:{
    tag(){
      // 顶部的精品歌单
      // 顶部的精品歌单
      this.topData()
      // 顶部的精品歌单
      this.listData()
      //修改页码为1
      this.page = 1
    }
  },
  created() {
    // 顶部的精品歌单
    this.topData()
    // 顶部的精品歌单
    this.listData()

  },
  methods: {
      //跳转歌单详情页
      toPlaylist(id){
          //跳转并携带数据 两种方法
          // this.$router.push('/playlist?q='+id)
          this.$router.push(`/playlist?q=${id}`)
      },
    // 抽取顶部数据
    topData(){
      // 顶部的精品歌单
      axios({
        url:' https://autumnfish.cn/top/playlist/highquality',
        method:'get',
        params:{
          limit:1,
          cat:this.tag
        }
      }).then(res => {
        // console.log(res.data)
        this.toplist = res.data.playlists[0]
      })
    },
    // 抽取列表数据
    listData(){
      //歌单列表
      axios({
        url:' https://autumnfish.cn/top/playlist/',
        method:'get',
        params:{
          limit:10,
          //起始的值
          offset:(this.page - 1)*10,
          //分类数据
          cat:this.tag
        }
      }).then(res => {
        // console.log(res)
        //保存总条数
        this.total = res.data.total
        this.list = res.data.playlists
      })
    },
    // 页码改变事件
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`);
      // 保存页码
      this.page = val
      //重新获取数据
      this.listData()
    }
  }
};
</script>

<style >

</style>
