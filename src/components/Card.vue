<template>

  <div class="my_card">
    <img class="card_cover" :src="cardCover" :alt="i === 'movies' ? element.title : element.name">
    <div class="card_info">
      {{ i === 'movies' ? element.title : element.name}}
      <ul>
        <li>
          {{i === 'movies' ? element.original_title : element.original_name}}
        </li>
        <li>
          <img class="langImg" :src="languageFlag" :alt="element.original_language">
        </li>
        <li>
          <i v-for="n in 5" :key="n" :class="n <= voteToStars ? 'fas fa-star' : 'far fa-star' "></i>
        </li>
      </ul>
    </div>
  </div>

</template>

<script>
export default {
  name: 'Card',
  props: {
    element: Object,
    i: String
  },
  computed: {
    cardCover() {
      if (this.element.poster_path) {
        return 'https://image.tmdb.org/t/p/' + 'w342' + this.element.poster_path
      } else {
        return 'https://vglist.co/assets/no-cover-60a919fca497ced5f84133c0ce073e17475c47f4a4cb122f2150299dc549d223.png'
      }
    },
    voteToStars() {
      return Math.round(this.element.vote_average / 2);
    },
    languageFlag() {
      const lang = this.element.original_language;
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
    }
  }
}
</script>