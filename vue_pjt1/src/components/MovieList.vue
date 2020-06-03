<template>
  <div v-if="initChk">
    <br/>
    <h2>나만의 무비 컬렉션</h2>
    <br/>
    <button type="button" class="btn btn-primary" @click="init">영화 가져오기</button>
  </div>

  <div v-else>
    <br/>
    <h2>나만의 무비 컬렉션</h2>
    <br/>
    <div class="container">
      <div class="row justify-content-center">
        <MovieListItem class="col-3" v-for="movie in movies" :key="movie.id" :movie="movie"/>
      </div>
    </div>
  </div>
</template>

<script>
import MovieListItem from '@/components/MovieListItem.vue'
import axios from 'axios'

const MOVIE_DATA_URL = 'http://www.json-generator.com/api/json/get/ceNyuXZmwi?indent=2'

export default {
  name: 'MovieList',
  data() {
    return {
      initChk: true,
      movies: null,
    }
  },
  components: {
    MovieListItem,
  },
  methods: {
    init() {
      // 영화 가져오기 버튼 누르면, 버튼을 없애고 movies에 데이터 할당
      this.initChk = false,
      axios.get(MOVIE_DATA_URL)
        .then((res)=>{
          this.movies = res.data
        })
    },
  },
}
</script>

<style>

</style>