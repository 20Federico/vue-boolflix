<template>
  <header class="d-flex justify-content-between align-items-center py-4 px-4 bg-black text-danger">
    <h1>BOOLFLIX</h1>
    <label @focus="formActive = true" @click="$emit('search', keyWord)" class="d-sm-none" for="search" tabindex="0"><i class="fas fa-search"></i></label>
    <form action="#" :class=" formActive ? 'form_active' : '' ">
      <input placeholder="cerca film o serie tv" @focusout="formActive = false" @keyup.enter="$emit('search', keyWord)"  id="search" type="text" v-model="keyWord" class="p-1 ps-2">
      <button @click="$emit('search', keyWord)" type="button" class="py-1 text-white bg-danger border-danger px-3 d-none d-sm-inline-block">Cerca</button>
    </form>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    return {
      keyWord: "",
      formActive: false
    }
  }
}
</script>