<template>
  <div id="app">
    <h1>Giphy API</h1>
    <search v-on:SearchRequested="handleSearch"></search>
    <p v-if="isLoading">Yükleniyor...</p>
    <preview :gifs="gifs"></preview>
  </div>
</template>

<script>

import Search from './components/Search.vue'
import Preview from './components/Preview.vue'


export default {
  name: 'app',
  components: { Search, Preview },
  data() {
    return {
      isLoading: true,
      gifs: []
    }
  },
  methods: {
    handleSearch(query) {
      this.gifs = [];
      this.isLoading =true;
      fetch(`http://api.giphy.com/v1/gifs/search?q=${query}&api_key=7P5Q4LuiR0MmWGusm8xwq2XBtWXpUVBs`)
        .then((res) => { return res.json() }) //response alığ json dönüyoruz
        .then((res) => { 
          this.gifs = res.data;
          this.isLoading = false;
        })
    }  
  },
  created(){ // uygulama açıldığı anda yani vue created edildiğinde çalışır
    fetch('http://api.giphy.com/v1/gifs/trending?api_key=7P5Q4LuiR0MmWGusm8xwq2XBtWXpUVBs')
    .then((res) => { return res.json() }) //response alığ json dönüyoruz
    .then((res) => { 
      this.gifs = res.data;
      this.isLoading = false;
    })
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
