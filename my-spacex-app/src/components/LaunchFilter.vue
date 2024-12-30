<template>
  <div class="filter mb-4">
    <label for="filter" class="block text-lg font-semibold mb-2">Filtrer les lancements :</label>
    <select
      id="filter"
      v-model="selectedFilter"
      @change="onFilterChange"
      class="border rounded-md p-2"
    >
      <option value="all">Tous les lancements</option>
      <option value="success">Lancements réussis</option>
      <option value="failure">Lancements échoués</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedFilter: 'all',
    };
  },
  methods: {
    onFilterChange() {
      this.$emit('filter-change', this.selectedFilter);
    },
  },
};
</script>
