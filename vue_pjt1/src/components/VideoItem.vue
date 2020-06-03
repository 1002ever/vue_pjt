<template>
  <div>
    <ul class="list-group">
      <VideoItemDetail v-for="video in videos" :key="video.etag" :video="video" @video-select="onVideoSelect"/>
    </ul>
  </div>
</template>

<script>
import VideoItemDetail from '@/components/VideoItemDetail.vue'

export default {
  name: 'VideoItem',
  props: {
    videos: {
      type: Array,
    }
  },
  components: {
    VideoItemDetail,
  },
  methods: {
    onVideoSelect(video) {
      this.$emit('video-select', video)
    }
  }
}
</script>

<style>

</style>