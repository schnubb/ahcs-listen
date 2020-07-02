<template>
  <div id="app">
    <MovieList title="Test" />
  </div>
</template>

<script>
  import MovieList from "./components/MovieList";

  export default {
  name: 'App',
  components: {
    MovieList
  }
}
</script>

<style>
  @import "~bootstrap/dist/css/bootstrap.min.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
