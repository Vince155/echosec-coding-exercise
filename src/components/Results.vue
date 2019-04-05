<template>
  <v-flex xs12 sm6>
    <v-card
      v-for="(result, index) in results"
      :key="index"
      class="search-result ma-3"
    >
      <!-- EXERCISE - Format search results -->
      <v-list>
        <v-list-tile>
          {{ result }}
        </v-list-tile>
      </v-list>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  name: "Results",
  props: {
    results: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
  .search-result {
    min-height: 100px;
  }
</style>
