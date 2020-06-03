<template>
  <li class="list-group-item" @click="onVideoSelect">
    <div class="container">
      <img :src="thumbnailUrl" alt="" class="m-auto">
      <p v-html="video.snippet.title"></p>
  
    </div>
  </li>
</template>

<script>
export default {
  name: 'VideoItemDetail',
  props: {
    video: {
      type: Object,
    }
  },
  computed: {
    thumbnailUrl() {
      return this.video.snippet.thumbnails.default.url
    }
  },
  methods: {
    onVideoSelect() {
      this.$emit('video-select', this.video)
    }
  }
}
</script>

<style>

</style>