<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm6>
      <v-form @submit.prevent="submitSearch">
        <v-text-field
          label="Search"
          prepend-inner-icon="search"
          single-line
          solo
          clearable
          v-model="searchInput"
        ></v-text-field>
      </v-form>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from "axios";

/**
 * @link https://anapioficeandfire.com/Documentation#characters
 */
const CHARACTERS_API_ENDPOINT = "https://www.anapioficeandfire.com/api/characters";

export default {
  name: "SearchBarInput",
  data: () => ({
    searchInput: ""
  }),
  methods: {
    /**
     * When the user submits their search request (hits enter) query the API endpoint
     */
    submitSearch() {
      this.$emit('search-submitted');

      axios
        .get(CHARACTERS_API_ENDPOINT, {
          params: {
            // EXERCISE - Implement query GET parameters to search by name. Watch for case sensitivity.
          },
        })
        .then(response => {
          // EXERCISE - Use the Vue.js bus (see eg: line 36 above) to emit a search-responded event with the results.
          console.log(response); // eslint-disable-line no-console
        });
    }
  }
};
</script>

<style scoped>
</style>