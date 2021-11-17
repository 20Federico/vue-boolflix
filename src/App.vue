<template>
  <div id="app">
    <label for="search">Cerca un film o una serie tv</label>
    <input @keyup.enter="searchContent"  id="search" type="text" v-model="keyWord">
    <button @click="searchContent" type="buttom">cerca</button>

    <ul>
      <li v-for="movie in movies" :key="movie.id">
        {{movie.title}}
        <ul>
          <li>{{movie.original_title}}</li>
          <li>{{movie.original_language}}</li>
          <li>{{movie.vote_average}}</li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
      apiKey: "74546dbedf2125e52d6aff0b896163c3",
      apiUrl: "https://api.themoviedb.org/3",
      movies: [],
      series: [],
      keyWord: ""
    }
  },
  methods: {
    apiCall(categoryToSearch) {
      axios.get(this.apiUrl + "/search/" + categoryToSearch, {
      params: {
        api_key: this.apiKey,
        query: this.keyWord,
        language: "it"
      }
    }).then(resp => {
      if ( categoryToSearch === 'movie') {
        this.movies = resp.data.results
      } else if (categoryToSearch === 'tv') {
        this.series = resp.data.results
      }

    });
    },
    searchContent() {
      this.apiCall('movie')
      this.keyWord = ""
    }
  }
}
</script>

<style lang="scss">

</style>
