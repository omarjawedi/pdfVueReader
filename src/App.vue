<template>
  <div id="app">
    <PdfViewer class="pdfContainer"></PdfViewer>
  </div>
</template>

<script>

import PdfViewer from './components/pdfViewer.vue';


export default {
  name: 'App',
  components: {

    PdfViewer
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.pdfContainer{
  margin: 40px;
  justify-content: center;
  height: 100vh;
}
</style>
