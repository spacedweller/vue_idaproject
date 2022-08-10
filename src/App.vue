
<template>
  <ItemCatalogue/>
</template>
<script>

import ItemCatalogue from './components/ItemCatalogue.vue'
export default {
  name: 'App',
  message: "",
  components: {
    ItemCatalogue,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #E5E5E5;
  padding: 32px;
}

html, body, #app {
    height: 100vh;
}

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&family=Source+Sans+Pro:wght@400;600&display=swap');

</style>
