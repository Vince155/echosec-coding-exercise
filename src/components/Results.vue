<template>
  <v-flex xs12 sm6>
    <v-card
      v-for="(result, index) in results"
      :key="index"
      class="search-result ma-3"
    >
      <!-- EXERCISE - Format search results -->
      <v-list six-line subheader>
        <v-list-tile>
          <v-list-tile-content>
            <v-list-tile-sub-title v-text="result.name"></v-list-tile-sub-title>
            <v-list-tile-sub-title v-text="result.alias"></v-list-tile-sub-title>
          </v-list-tile-content>
          <v-list-tile-content>
            <v-list-tile-sub-title v-text="result.allegiance"></v-list-tile-sub-title>
          </v-list-tile-content>
          <v-list-tile-content>
            <v-list-tile-sub-title v-text="result.born"></v-list-tile-sub-title>
            <v-list-tile-sub-title v-text="result.died"></v-list-tile-sub-title>
            <v-list-tile-sub-title v-text="result.gender"></v-list-tile-sub-title>
            <v-list-tile-sub-title v-text="result.culture"></v-list-tile-sub-title>
          </v-list-tile-content>
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
