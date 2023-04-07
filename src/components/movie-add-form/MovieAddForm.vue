<template>
  <Box class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <Input
        type="text"
        class="form-control new-movie-label"
        placeholder="Qanday kino?"
        v-model="name"
      />
      <Input
        type="number"
        class="form-control new-movie-label"
        placeholder="Nechi marotaba ko'rilgan?"
        v-model="viewers"
      />
      <PrimaryButton class="btn-outline-dark" type="submit" @click="addMovie">
        Qo'shish
      </PrimaryButton>
    </form>
  </Box>
</template>

<script>
export default {
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      name: '',
      viewers: '',
    }
  },
  methods: {
    addMovie() {
      if (!this.name && !this.viewers) return
      const newMovie = {
        id: this.movies[this.movies.length - 1].id + 1,
        name: this.name,
        viewers: this.viewers,
        favourite: false,
        like: false,
      }
      this.$emit('createMovie', newMovie)
      this.name = ''
      this.viewers = ''
    },
  },
}
</script>

<style scoped>
.movie-add-form {
  margin-top: 2rem;
}
</style>
