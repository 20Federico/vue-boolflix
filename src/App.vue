<template>
  <div id="app">
    <label for="search">Cerca un film o una serie tv</label>
    <input @keyup.enter="searchContent"  id="search" type="text" v-model="keyWord">
    <button @click="searchContent" type="buttom">cerca</button>
    
    <div class="container" v-for="(category, i) in categories" :key="i">
      <h3 class="py-3 fs-1" v-if="category.length > 0">{{i.toUpperCase()}}</h3>
      <div class="d-flex flex-wrap mb-5">
        <div class="my_card" v-for="element in category" :key="element.id">
          <img class="card_cover" :src="cardCover(element.poster_path)" :alt="i === 'movies' ? element.title : element.name">
          <div class="card_info">
            {{ i === 'movies' ? element.title : element.name}}
            <ul>
              <li>{{i === 'movies' ? element.original_title : element.original_name}}</li>
              <li><img class="langImg" :src="languageFlag(element.original_language)" :alt="element.original_language"></li>
              <li>
                <i v-for="n in 5" :key="n" :class="n < voteToStars(element.vote_average) ? 'fas fa-star' : 'far fa-star' "></i>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script>
import axios from "axios";
import "@fortawesome/fontawesome-free/js/all.js";

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
      langFlagSrc: "",
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
      if (lang === "en") {
        return "https://upload.wikimedia.org/wikipedia/en/thumb/a/ae/Flag_of_the_United_Kingdom.svg/1200px-Flag_of_the_United_Kingdom.svg.png"
      } else if (lang === "it") {
        return "https://upload.wikimedia.org/wikipedia/en/thumb/0/03/Flag_of_Italy.svg/255px-Flag_of_Italy.svg.png"
      } else if (lang === "fr") {
        return "https://upload.wikimedia.org/wikipedia/commons/6/62/Flag_of_France.png"
      } else if (lang === "es") {
        return "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Flag_of_Spain.svg/2560px-Flag_of_Spain.svg.png"
      } else if (lang === "de") {
        return "https://upload.wikimedia.org/wikipedia/commons/thumb/b/ba/Flag_of_Germany.svg/2560px-Flag_of_Germany.svg.png"
      } else {
        return "https://upload.wikimedia.org/wikipedia/commons/2/2f/Missing_flag.png"
      }
    },
    cardCover(path) {
      if (path) {
        return 'https://image.tmdb.org/t/p/' + 'w342' + path
      } else {
        return 'https://vglist.co/assets/no-cover-60a919fca497ced5f84133c0ce073e17475c47f4a4cb122f2150299dc549d223.png'
      }
    },
    // takes decimal from 0 to 10 and and converts it to int from 0 to 5
    voteToStars(vote) {
      return Math.round(vote / 2);
    }
  }
}
</script>

<style lang="scss">
  @import '@/styles/app';
</style>
