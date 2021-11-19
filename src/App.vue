<template>
  <div id="app">

    <Header @search="keyWord = $event"></Header>
    <Main :keyWord="keyWord" ></Main>
    
  </div>
</template>

<script>
import "@fortawesome/fontawesome-free/js/all.js";
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: { 
    Header,
    Main
  },
  data() {
    return {
      keyWord: ""
    }
  }
}
</script>

<style lang="scss">
  @import '@/styles/app';
</style>
