<template>
  <div>
    <div class="container" v-for="(category, i) in categories" :key="i">
      <h3 class="py-3 fs-1" v-if="category.length > 0">{{i.toUpperCase()}}</h3>
      <div class="d-flex flex-wrap mb-5">
        
        <Card v-for="element in category" :key="element.id" :element="element" :i="i" ></Card>

      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Card from './Card.vue';

export default {
  components: { Card },
  name: 'CardsContainer',
  props: {
    keyWord: String
  },
  data() {
    return {
      apiKey: "74546dbedf2125e52d6aff0b896163c3",
      apiUrl: "https://api.themoviedb.org/3",
      categories: {
        movies: [],
        series: []
      },
    }
  },
  methods: {
    apiCall(categoryToSearch, query) {
      axios.get(this.apiUrl + "/search/" + categoryToSearch, {
      params: {
        api_key: this.apiKey,
        query: query,
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

    searchContent(keyWord) {
      this.apiCall('movie', keyWord)
      this.apiCall('tv', keyWord)
    }
  },
  watch: {
    keyWord: function(newKeyWord) {
      this.searchContent(newKeyWord)
    }
  }
}
</script>