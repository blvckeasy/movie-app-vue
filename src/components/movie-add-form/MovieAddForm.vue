<template>
  <div class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <input
        type="text"
        class="form-control new-movie-label"
        placeholder="Qanday kino?"
        :value="name"
        @input="name = $event.target.value"
      />
      <input
        type="number"
        class="form-control new-movie-label"
        placeholder="Nechi marotaba ko'rilgan?"
        :value="viewers"
        @input="viewers = $event.target.value"
      />
      <button class="btn btn-outline-dark" type="submit" @click="addMovie">Qo'shish</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    movies: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {
      name: '',
      viewers: '',
      response: null
    }
  },
  methods: {
    addMovie () {
      if (!this.name && !this.viewers) return;
      const newMovie = {
        id: this.movies[this.movies.length - 1].id + 1,
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false, 
      }
      this.$emit("createMovie", newMovie) 
      this.name = ''
      this.viewers = '' 
    }, 
  }
}
</script>

<style scoped>
.movie-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
