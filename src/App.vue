<template>
  <div id="app">
    <div class="container">
      <!-- 1-3. 호출하시오. 
        필요한 경우 props를 데이터를 보내줍니다.
      -->
      <MovieList :genres="genres" :movies="movies" />
    </div>
  </div>
</template>

<script>
import MovieList from "./components/movies/MovieList";
const axios = require("axios");
// 1-1. 저장되어 있는 MovieList 컴포넌트를 불러오고,

export default {
  name: "app",
  // 1-2. 아래에 등록 후
  components: {
    MovieList
  },
  data() {
    return {
      // 활용할 데이터를 정의하시오.
      movies: [],
      genres: []
    };
  },
  mounted() {
    // 0. mounted 되었을 때,
    // 1) 제시된 URL로 요청을 통해 data의 movies 배열에 해당 하는 데이터를 넣으시오.
    // 2) 제시된 URL로 요청을 통해 data의 genres 배열에 해당 하는 데이터를 넣으시오.
    // axios는 위에 호출되어 있으며, node 설치도 완료되어 있습니다.
    const MOVIE_URL =
      "https://gist.githubusercontent.com/mandaringit/3efce7a2aab3f03c0d4dfdeafffbebd9/raw/c06ba751908182026226718786d40b7536cec4fd/movie.json";
    const GENRE_URL =
      "https://gist.githubusercontent.com/mandaringit/4f81bc173ed897b33c0f57647decdc9a/raw/0fbc99ee7f4fb72b9a0dd25959ce7c8f32bf7b22/genre.json";
    axios
      .get(MOVIE_URL)
      .then(res => {
        const { data } = res;
        this.movies = data;
      })
      .catch(err => console.log(err));

    axios
      .get(GENRE_URL)
      .then(res => {
        const { data } = res;
        this.genres = data;
      })
      .catch(err => console.log(err));
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
