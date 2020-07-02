<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-6">
                <div class="input-group">
                    <input class="form-control" type="text" v-model="search" />
                </div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item" v-for="movie in filteredMovies" :key="movie.id">
                        <h3>{{movie.title}}</h3>
                        <h4 v-if="movie.subtitle">{{movie.subtitle}}</h4>
                        <p v-if="movie.director.length">
                            <span v-for="(artist, index) in movie.director" :key="artist.id">
                                {{index === (movie.director.length -1 ) ? artist.showName : artist.showName + ","}}
                            </span>
                        </p>
                    </li>
                </ul>
            </div>
        </div>
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
        query: `query { movies { id, title, subtitle, director { id, showName } } }`
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