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
const HOUSES_API_ENDPOINT = "https://www.anapioficeandfire.com/api/houses";
const BOOKS_API_ENDPOINT = "https://www.anapioficeandfire.com/api/books";

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
            name: this.searchInput,
            aliases: this.searchInput
          },
        })
        .then(response => {
          // EXERCISE - Use the Vue.js bus (see eg: line 36 above) to emit a search-responded event with the results.
          /**
           * this.emit triggers a function to be called on App.vue with the API response as a parameter to use
           * on searchResponded
           */
          this.$emit('search-responded', response.data);
        });
    }
  }
};
</script>

<style scoped>
</style>