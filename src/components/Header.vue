<template>
  <header class="d-flex justify-content-between align-items-center py-4 px-4 bg-black text-danger">
    <h1>BOOLFLIX</h1>
    <form action="#">
      <input placeholder="cerca film o serie tv" @keyup.enter="$emit('search', keyWord)"  id="search" type="text" v-model="keyWord" class="p-1 ps-2">
      <button @click="$emit('search', keyWord)" type="button" class="py-1 text-white bg-danger border-danger px-3">Cerca</button>
    </form>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      keyWord: ""
    }
  }
}
</script>