<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo
        :allMoviesCount="movies.length"
        :favouriteMoviesCount="movies.filter(o => o.favourite).length"
      />
      <div class="search-panel">
        <SearchPanel :updateTermHandler="updateTermHandler" />
        <AppFilter
          :updateFilterHandler="updateFilterHandler"
          :filterName="filter"
        />
      </div>
      <MovieList
        :movies="onFilterHandler(onSearchHandler(movies, term), filter)"
        @onToggle="onToggleHandler"
        @onRemove="onRemoveHandler"
      />
      <MovieAddForm @createMovie="createMovie" :movies="movies" />
    </div>
  </div>
</template>

<script>
import AppInfo from '@/components/app-info/AppInfo.vue'
import SearchPanel from '@/components/search-panel/SearchPanel.vue'
import AppFilter from '@/components/app-filter/AppFilter.vue'
import MovieList from '@/components/movie-list/MovieList.vue'
import MovieAddForm from '@/components/movie-add-form/MovieAddForm.vue'

export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
  },
  data() {
    return {
      movies: [
        { id: 1, name: 'Omar', viewers: 811, favourite: false, like: true },
        {
          id: 2,
          name: 'Empire of osman',
          viewers: 141,
          favourite: true,
          like: false,
        },
        { id: 3, name: 'Ertugrul', viewers: 1267, favourite: true, like: true },
      ],
      term: '',
      filter: 'all',
    }
  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
    },
    onToggleHandler(params) {
      this.movies = this.movies.map(item => {
        if (item.id === params.id) {
          item[params.prop] = !item[params.prop]
        }
        return item
      })
    },
    onRemoveHandler(id) {
      this.movies = this.movies.filter(c => c.id !== id)
    },
    onSearchHandler(arr, term) {
      if (!term.length) return arr
      return arr.filter(
        c => c.name.toLowerCase().indexOf(term.toLowerCase()) > -1
      )
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'popular':
          return arr.filter(c => c.like)
        case 'mostViewers':
          return arr.filter(c => c.viewers > 500)
        default:
          return arr
      }
    },
    updateTermHandler(term) {
      this.term = term
    },
    updateFilterHandler(filter) {
      this.filter = filter
    },
  },
}
</script>

<style>
.app {
  height: 100vh;
  color: black;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0px;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
