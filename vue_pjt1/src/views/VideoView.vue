<template>
  <div id="app">
    <div class="container">
      <h1>영화 예고편 검색</h1>
      <VideoSearch class="" @search-list="onSearchList"/>
      <div class="row">
        <VideoItem class='col-12' v-bind:videos="videos" @video-select="onVideoSelect"/>
      </div>
    </div>
  </div>
</template>

<script>

import VideoSearch from '@/components/VideoSearch.vue'
import VideoItem from "@/components/VideoItem.vue"
import axios from 'axios'

const API_KEY = process.env.VUE_APP_API_KEY
const YOUTUBE_URL = 'https://www.googleapis.com/youtube/v3/search'

export default {
  name: 'VideoView',
  components: {
    VideoSearch,
    VideoItem,
  },
  data() {
    return {
      videos: [],
      selectedVideo: null,
    }
  },
  methods: {
    onSearchList(input) {
      if(input != false) {
        const params = {
          key: API_KEY,
          part: 'snippet',
          type: 'video',
          // trailer 를 붙여서 검색
          q: input + ' trailer',
        }
        axios.get(YOUTUBE_URL, {params})
          .then((res)=>{
            this.videos = res.data.items
          }).catch(err => {console.log(err)})
      }
    },
    onVideoSelect(video){
      this.selectedVideo = video
    }
  }
}
</script>

<style>

</style>