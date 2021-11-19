<template>
  <main>
    <CardsContainer :keyWord="keyWord"></CardsContainer>
  </main>
</template>

<script>
import CardsContainer from './CardsContainer.vue';

export default {
  components: { CardsContainer },
  name: 'Main',
  props: {
    keyWord: String
  }
}
</script>
