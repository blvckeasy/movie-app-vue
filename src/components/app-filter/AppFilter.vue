<template>
  <div class="btn-group">
    <PrimaryButton
      v-for="btn in filterButtons"
      :key="btn.name"
      :class="[filterName === btn.name ? 'btn-dark' : 'btn-outline-dark']"
      @click="filterHandler(btn.name)"
    >
      {{ btn.title }}
    </PrimaryButton>
  </div>
</template>

<script>
export default {
  props: {
    updateFilterHandler: {
      type: Function,
      required: true,
    },
    filterName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      filter: 'all',
      filterButtons: [
        {
          title: 'Barcha kinolar',
          name: 'all',
        },
        {
          title: 'Mashxur kinolar',
          name: 'popular',
        },
        {
          title: "Eng ko'p ko'rilgan kinolar",
          name: 'mostViewers',
        },
      ],
    }
  },
  methods: {
    filterHandler(filter) {
      this.filter = filter
      this.updateFilterHandler(this.filter)
    },
  },
}
</script>

<style scoped></style>
