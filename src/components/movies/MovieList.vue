<template>
  <div>
    <h1>영화 목록</h1>
    <h2>장르 선택</h2>

    <select class="form-control" v-model="selectedGenreId">
      <option value="default">전체보기</option>
      <option v-for="genre in genres" :key="genre.id" :value="genre.id">{{genre.name}}</option>
    </select>

    <div class="row">
      <MovieListItem v-for="movie in computedMoviesByGenreId" :movie="movie" :key="movie.id" />
    </div>
  </div>
</template>

<script>
// 1-1. 저장되어 있는 MovieListItem 컴포넌트를 불러오고,
import MovieListItem from "./MovieListItem";

export default {
  name: "MovieList",
  // 1-2. 아래에 등록 후
  components: {
    MovieListItem
  },
  // 0. props 데이터를 받이 위하여 설정하시오.
  // genres와 movies 모두 타입은 Object이며, 필수입니다.
  // 설정이 완료 되었다면, 상위 컴포넌트에서 값을 넘겨 주세요.
  // 그리고 적절한 곳에 사용하세요.
  props: {
    genres: {
      type: Array,
      required: true
    },
    movies: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      selectedGenreId: "default"
    };
  },
  // 2-3.에서 이야기하는 특정한 함수는 selectedGenreId의 값이 변경될 때마다 호출 됩니다.
  // 드랍다운에서 장르를 선택하면, 해당 영화들만 보여주도록 구현 예정입니다.
  // 주의할 것은 직접 부모 컴포넌트의 데이터를 변경할 수 없다는 점입니다.
  // 완료 후
  computed: {
    computedMoviesByGenreId() {
      if (this.selectedGenreId === "default") return this.movies;
      return this.movies.filter(
        movie => movie.genre_id === this.selectedGenreId
      );
    }
  }
};
</script>

<style>
select {
  display: block;
  width: 50% !important;
  margin: 2rem auto !important;
}
</style>