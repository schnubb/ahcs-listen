<template>
    <div class="random-div">
        <input type="text" v-model="search" />
        <ul>
            <li v-for="movie in filteredMovies" :key="movie.id">
                {{movie.title}} || {{movie.subtitle}}
            </li>
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
      loading: true,
      search: ""
    }
  },
  props: {
    title: String
  },
    methods: {
    },
  computed: {
    filteredMovies: function() {
      const self = this;
      return self.movies.filter(movie => {
        if (self.search !== "") {
          const searchString = self.search.toLowerCase();
          const subtitle = (movie.subtitle || "").toLowerCase();
          const title = movie.title.toLowerCase();
          return title.includes(searchString) || subtitle.includes(searchString);
        }
        return true;
      });
    }
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