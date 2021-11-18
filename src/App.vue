<template>
  <div id="app">
    <label for="search">Cerca un film o una serie tv</label>
    <input @keyup.enter="searchContent"  id="search" type="text" v-model="keyWord">
    <button @click="searchContent" type="buttom">cerca</button>

    <ul v-for="(category, i) in categories" :key="i">
    <h3 v-if="category.length > 0">{{i.toUpperCase()}}</h3>
      <li v-for="element in category" :key="element.id">
        <span v-if="i === 'movies'">{{element.title}}</span>
        <span v-if="i === 'series'">{{element.name}}</span>
        <ul>
          <li v-if="i === 'movies'">{{element.original_title}}</li>
          <li v-if="i === 'series'">{{element.original_name}}</li>
          <li><img style="width: 20px" :src="languageFlag(element.original_language)" :alt="element.original_language"></li>
          <li>{{element.vote_average}}</li>
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
      categories: {
        movies: [],
        series: []
      },
      keyWord: "",
      langFlagSrc: ""
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
        this.categories.movies = resp.data.results
      } else if (categoryToSearch === 'tv') {
        this.categories.series = resp.data.results
      }
    });
    },
    searchContent() {
      this.apiCall('movie')
      this.apiCall('tv')
      // this.keyWord = ""
    },
    languageFlag(lang) {
      switch (lang) {
        case "en":
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/en/thumb/a/ae/Flag_of_the_United_Kingdom.svg/1200px-Flag_of_the_United_Kingdom.svg.png"
        break;

        case "it":
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/en/thumb/0/03/Flag_of_Italy.svg/255px-Flag_of_Italy.svg.png"
        break;

        case "fr":
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/commons/6/62/Flag_of_France.png"
        break;

        case "es":
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/2560px-Flag_of_Spain.svg.png"
        break;

        case "de":
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/2560px-Flag_of_Germany.svg.png"
        break;
        
        default: 
        this.langFlagSrc = "https://upload.wikimedia.org/wikipedia/commons/2/2f/Missing_flag.png"
        break;
        
      }
      return this.langFlagSrc
    }
  }
}
</script>

<style lang="scss">

</style>
