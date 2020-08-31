<template>
  <div id="app">
    <Gallery/>
  </div>
</template>

<script> 

import Gallery from './components/Gallery/index.vue'

export default {
  name: 'App',
  components: {
    Gallery
  }
}
</script>

<style>
 * {
   box-sizing: border-box;
   margin: 0;
   padding: 0;
 }

 body{
    font-family: 'Poppins', sans-serif;
    line-height: 1.4;
    color: #212121;
    font-size: 16px;
 }
</style>
