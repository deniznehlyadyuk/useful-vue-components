<template>
  <div id="selectedFilterApp">
    <v-chip-group>
      <v-chip
        v-for="filter in dataSource"
        :key="filter.id + filter.name"
        class="mr-1"
        label
        close
        @click:close="unselectFilter(filter)"
      >
        {{ filter.name }}
      </v-chip>
    </v-chip-group>
  </div>
</template>

<script>
export default {
  name: 'SelectedFilterChips',
  props: {
    dataSource: {
      type: Array,
      required: true
    }
  },
  methods: {
    unselectFilter (filter) {
      this.$emit('unselect-filter', filter)
    }
  }
}
</script>

<style scoped>

</style>
