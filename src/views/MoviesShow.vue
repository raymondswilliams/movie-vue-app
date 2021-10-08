<template>
  <div class="movies-show">
    <h4>{{ movie.title }}</h4>
    <p>plot: {{ movie.plot }}</p>
    <p>year: {{ movie.year }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <button v-on:click="destroyMovie">Delete</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: [],
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
