<template>
  <v-app>
    <v-toolbar app>
      <search-bar-input
        v-on:search-submitted="isLoading = true"
        v-on:search-responded="searchResponded"
      />
    </v-toolbar>
    <v-content>
      <v-layout justify-center>
        <!-- Loading spinner -->
        <v-progress-circular
          v-if="isLoading"
          indeterminate
          class="mt-5"
        ></v-progress-circular>
        <!-- Search results -->
        <results
          v-else
          :results="results"
        />
      </v-layout>
    </v-content>
  </v-app>
</template>

<script>
import SearchBarInput from "./components/SearchBarInput";
import Results from "./components/Results";

export default {
  name: "App",
  components: {
    SearchBarInput,
    Results
  },
  data: () => ({
    isLoading: false,
    // An array of Song of Ice and Fire Characters to display
    results: []
  }),
  methods: {
    /**
     * When the API responds, display search results
     * @param {object} response - API response
     */
    searchResponded(response) {
      this.isLoading = false;

      // EXERCISE - Implement logic to handle the API response.
      console.log(response); // eslint-disable-line no-console
    }
  }
};
</script>
