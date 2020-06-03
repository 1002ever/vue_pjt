<template>
  <div>
    <div v-if="selectedVideo">
      <div class="embed-responsive embed-responsive-16by9">
        <iframe class="embed-responsive-item" :src="videoSrc" allowfullscreen></iframe>
      </div>
      <h4 v-html="selectedVideo.snippet.title"></h4>
      <p>{{ selectedVideo.snippet.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    selectedVideo: {
      type: Object,
    }
  },
  computed: {
    videoSrc() {
      return `https://www.youtube.com/embed/${this.selectedVideo.id.videoId}` // 백팁(python의 f-string 느낌)
    }
  }
}
</script>

<style>

</style>