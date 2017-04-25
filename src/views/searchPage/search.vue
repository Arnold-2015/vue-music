<template lang="html">
  <transition name="showRouter">
    <div class="find">
      <div class='header-other'>
        <span @click="goBack" class="back"><i class="back-icon"></i></span>
        <div class="input">
          <input v-model="keywords" @keyup.enter="toSearch(keywords)" type="text"  placeholder='搜素音乐、歌手、歌词、用户'>
          <!--<i @click="keywords=''" v-show="keywords!==''&&!isShowHot" class="icon-cancel"></i>-->
        </div>
      </div>
      <div class="hot" v-if="isShowHot">
        热门搜索
        <!--<div class="keywords">-->
          <!--<div v-for="item of hotKeywords" v-text="item" @click="toSearch(item)" class="keyword"></div>-->
        <!--</div>-->
      </div>
      <div v-else class="search-list">
        <!--<div class="fixed-bar">-->
          <!--<mu-tabs :value="activeTab" @change="handleTabChange" class="view-tabs">-->
            <!--<mu-tab value="singleList" title="单曲"/>-->
            <!--<mu-tab value="singerLists" title="歌手"/>-->
            <!--<mu-tab value="albumLists" title="专辑"/>-->
            <!--<mu-tab value="playLists" title="歌单"/>-->
            <!--<mu-tab value="userLists" title="用户"/>-->
          <!--</mu-tabs>-->
        <!--</div>-->
        <div class="fixed-bar">
          <mt-button @click.native.prevent="active = 'single'">单曲</mt-button>
          <mt-button @click.native.prevent="active = 'singer'">歌手</mt-button>
          <mt-button @click.native.prevent="active = 'album'">专辑</mt-button>
          <mt-button @click.native.prevent="active = 'playlist'">歌单</mt-button>
          <mt-button @click.native.prevent="active = 'user'">用户</mt-button>
        </div>
        <mt-tab-container class="page-tabbar-tab-container" v-model="active" swipeable>
          <mt-tab-container-item id="single">
            <v-single-list></v-single-list>
          </mt-tab-container-item>
          <mt-tab-container-item id="singer">
            <v-singer-list></v-singer-list>
          </mt-tab-container-item>
          <mt-tab-container-item id="album">
            <v-album-list></v-album-list>
          </mt-tab-container-item>
          <mt-tab-container-item id="playlist">
            <v-play-list></v-play-list>
          </mt-tab-container-item>
          <mt-tab-container-item id="user">
            <v-user-list></v-user-list>
          </mt-tab-container-item>
        </mt-tab-container>
      </div>
    </div>
  </transition>
</template>
<script>
  import vSingleList from './list/SingleList.vue';
  import vSingerList from './list/SingerList.vue';
  import vAlbumList from './list/AlbumList.vue';
  import vPlayList from './list/PlayList.vue';
  import vUserList from './list/UserList.vue';
  export default {
    name: 'search',
    data () {
      return {
        keywords: '',
        isShowHot: true,
        active: 'single'
      };
    },
    methods: {
      goBack () {
        this.$router.push({
          path: '/find'
        });
      },
      toSearch (keywords) {
        this.isShowHot = false;
        if (this.keywords.trim()) {
          this.activeTab = 'singleList';
          this.$router.push({
            path: '/search/singleList',
            query: {
              keywords: keywords
            }
          });
        }
      }
    },
    components: {
      vSingleList,
      vSingerList,
      vAlbumList,
      vPlayList,
      vUserList
    }
  };
</script>
<style lang="stylus" rel="stylesheet/stylus">
  @import "search.styl";
</style>
