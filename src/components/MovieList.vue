<template>
    <div class="random-div">
        <ul>
            <li v-for="movie in movies" v-bind="movies" :key="movie.id">{{movie.title}}</li>
        </ul>
    </div>
</template>

<script>
  import { graphcms } from "../../package.json";

  export default {
  name: "MovieList",
  data() {
    return {
      movies: [],
      errors: [],
      loading: false
    }
  },
  props: {
    title: String
  },
  methods: {
  },
  computed() {
  },
  mounted() {
  },
  async created() {
    const response = await fetch(graphcms.api, {
      method: "post",
      body: JSON.stringify({
        query: `query { movies { id, title, subtitle } }`
      })
    });

    const { data } = await response.json();

    this.errors = data.errors;
    this.loading = false;
    this.movies = data.movies;
  }
}
</script>

<style>

</style>