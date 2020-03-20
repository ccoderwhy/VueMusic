<template>
  <div class="index-container">
    <div class="nav" >
      <ul>
        <li>
          <router-link to="/discovery">
            <span class="iconfont icon-find-music"></span>
            发现音乐
          </router-link>
        </li>
        <li>
          <router-link to="/playlists">
            <span class="iconfont icon-music-list"></span>
            推荐歌单
          </router-link>
        </li>
        <li>
          <router-link to="/songs">
            <span class="iconfont icon-music"></span>
            最新音乐
          </router-link>
        </li>
        <li>
          <router-link to="/mvs">
            <span class="iconfont icon-mv"></span>
            最新MV
          </router-link>
        </li>
      </ul>
    </div>
    <div class="main">
      <router-view></router-view>
    </div>
<!--    //播放-->
    <div class="player">
<!--      autoplay自动播放-->
      <audio :src='musicUrl' autoplay controls></audio>
    </div>
  </div>
</template>

<script>
export default {
  name: 'index',
  data() {
    return {
      musicUrl:"http://m801.music.126.net/20200319184644/8ea5960ec565eddb44e57471c5e9f387/jdymusic/obj/w5zDlMODwrDDiGjCn8Ky/1591552905/f44c/1dc6/9cb1/070cfa0cd0d42def4a5634093989e9a7.mp3"
      // musicUrl:"http://m701.music.126.net/20200319184429/74abb1e8982d9aa8e81874cedb4ddfed/jdymusic/obj/w5zDlMODwrDDiGjCn8Ky/1629447477/6d6c/14eb/5e62/29367a07955bac2616ede523028e9d69.mp3"
      // musicUrl:"http://m801.music.126.net/20200319181341/3bcd581e8612ab092247850195ae0522/jdymusic/obj/w5zDlMODwrDDiGjCn8Ky/1629447477/6d6c/14eb/5e62/29367a07955bac2616ede523028e9d69.mp3"
      // musicUrl:"http://m7.music.126.net/20200303182550/8aa5971b1630d1527a922ccd2b97f392/ymusic/035d/0109/520e/478f86cc9f6c6539f7c8ed3e06c1bf8e.mp3"
    };
  }
};
</script>

<style >

</style>
