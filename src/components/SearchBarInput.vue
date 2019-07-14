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
//const HOUSES_API_ENDPOINT = "https://www.anapioficeandfire.com/api/houses";
//const BOOKS_API_ENDPOINT = "https://www.anapioficeandfire.com/api/books";

export default {
  name: "SearchBarInput",
  data: () => ({
    searchInput: "",
    characterName: [],
    finalChar: [],
    allegiances: [],
    results: []
  }),
  methods: {
    /**
     * When the user submits their search request (hits enter) query the API endpoint
     */
    async submitSearch() {
      this.$emit('search-submitted');

      await axios
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
          this.results = response.data;
          
          console.log('main search', this.results); // eslint-disable-line no-console

          for(var i = 0; i < this.results.length; i++) {
            // characters with allegiances can be taken down in a different list so
            // that they can match with allegiance list
            
            if(this.results[i].aliases.length === 0) var alias = "";
            else alias = this.results[i].aliases[0];
            if(this.results[i].name === "") var name = "";
            else name = this.results[i].name;
            if(this.results[i].allegiances.length === 0) this.allegiances[i] = "";
            else this.allegiances[i] = this.results[i].allegiances;

            this.characterName[i] = {
              alias: alias,
              name: name,
              allegiance: this.allegiances[i],
              born: this.results[i].born,
              died: this.results[i].died,
              culture: this.results[i].culture,
              gender: this.results[i].gender
            };
            console.log('charName', this.characterName[i]); // eslint-disable-line no-console
          }
          return this.characterName;
        });
        for(var i = 0; i < this.characterName.length; i++) {
          await axios
            .get(this.characterName[i].allegiance[0])
            .then(response => {
              console.log(response.data); // eslint-disable-line no-console
              this.characterName[i].allegiance = response.data.name;
            })
            .catch(error => {
              console.log(error); // eslint-disable-line no-console
              this.characterName[i].allegiance = "";
            });
        }

      console.log('charNameOut', this.characterName); // eslint-disable-line no-console
          
      this.$emit('search-responded', this.characterName);
    }
  }
};
</script>

<style scoped>
</style>