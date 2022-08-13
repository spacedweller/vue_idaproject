<template>
<div v-cloak>
  <StoreCatalogue/>
</div>

</template>
<script>

import StoreCatalogue from './components/StoreCatalogue.vue'
export default {
  name: 'App',
  message: "",
  components: {
    StoreCatalogue,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #faf9f7;
  padding: 32px;
}

html, body, #app {
    box-sizing: border-box;
    min-width:360px;        
    width: auto !important; 
}

    [v-cloak] {
    display: block;
    padding: 50px 0;
}

@keyframes spinner {
    to {
        transform: rotate(360deg);
    }
}

[v-cloak]:before {
    content: "";
    box-sizing: border-box;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 20px;
    height: 20px;
    margin-top: -10px;
    margin-left: -10px;
    border-radius: 50%;
    border: 2px solid #ccc;
    border-top-color: #333;
    animation: spinner 0.6s linear infinite;
    text-indent: 100%;
    white-space: nowrap;
    overflow: hidden;
}

[v-cloak]>* {
    display: none;
}

</style>
