<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    <div>Search: <input type="text" v-model="titleFilter" list="titles" /></div>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <div>
      <button v-on:click="sortAlphabetically = 'title'">Sort by Title</button>
    </div>
    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        sortAlphabetically
      )"
      v-bind:key="movie.id"
    >
      <h4>{{ movie.title }}</h4>
      <p>plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">See Details</router-link>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      sortAlphabetically: "",
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
