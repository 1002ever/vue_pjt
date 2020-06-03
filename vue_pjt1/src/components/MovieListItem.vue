<template>
  <div>
    <div class="card" style="width: 18rem;">
      <img :src="movie.poster_url" class="card-img-top" alt="영화_이미지">
      <div class="card-body">
        <h5 class="card-title">{{ movie.title }}</h5>
        <button type="button" class="btn btn-warning" data-toggle="modal" :data-target="'#movie'+movie.id">영화 정보 상세보기</button>
        <MovieListItemModal :movie="movie"/>
      </div>
    </div>
  </div>
</template>

<script>
import MovieListItemModal from '@/components/MovieListItemModal.vue'

export default {
  name: 'MovieListItem',
  components: {
    MovieListItemModal,
  },
  props: {
    movie: {
      type: Object,
    },
  },
}
</script>

<style>
</style>