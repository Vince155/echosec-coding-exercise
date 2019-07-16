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
    searchInput: "",
    characterName: [],
    allegiances: [],
    aliasFirst: "",
    results: []
  }),
  methods: {
    /**
     * When the user submits their search request (hits enter) query the API endpoint
     */
    async submitSearch() {
      this.$emit('search-submitted');
      this.characterName = [];
      this.allegiances = [];

      await axios
        .get(CHARACTERS_API_ENDPOINT, {
          params: {
            // EXERCISE - Implement query GET parameters to search by name. Watch for case sensitivity.
            aliases: this.searchInput
          },
        })
        .then(response => {
          // EXERCISE - Use the Vue.js bus (see eg: line 36 above) to emit a search-responded event with the results.
          
          // The response is stored in the this.results list
          this.results = response.data;
          this.searchInput = this.searchInput.toLowerCase().split(' ');
          for(var h = 0; h < this.searchInput.length; h++) {
            this.searchInput[h] = this.searchInput[h].charAt(0).toUpperCase() + this.searchInput[h].substring(1);
          }
          this.searchInput = this.searchInput.join(' ');
          if(this.searchInput === "The Daughter Of The Dusk") this.searchInput = "The Daughter of the Dusk";
          if(this.searchInput === "The Sailor's Wife" || this.searchInput === "The Sailors Wife") {
            this.searchInput = "the Sailor's Wife";
          }
          console.log('search input', this.searchInput);
          return this.results;
        });

      if(this.searchInput !== "") {
        for(var x = 0; x < this.results.length; x++) {
          console.log('result index', this.results[x].aliases[0]);
          if(this.searchInput === this.results[x].aliases[0]) {
            this.results = this.results[x];
          }
          else continue;
        }
        var alias = this.results.aliases[0];

        if(this.results.name === "") var name = "";
        else name = this.results.name;

        if(this.results.allegiances.length === 0) this.allegiances[0] = "";
        else this.allegiances[0] = this.results.allegiances;

        this.characterName[0] = {
          alias: alias,
          name: name,
          allegiance: this.allegiances[0],
          born: this.results.born,
          died: this.results.died,
          culture: this.results.culture,
          gender: this.results.gender
        };
      }

      console.log('alias search', this.results);
      console.log('alias search length', this.results.length);

      for(i = 0; i < this.results.length; i++) {
        console.log('new results', this.results);
        // The alias of a character is taken down depending on whether or not the character has one
        alias = this.results[i].aliases[0];

        /** 
         * Not every character has a name so the variable name will either the be an empty string 
         * or the name of result's index
         */
        if(this.results[i].name === "") name = "";
        else name = this.results[i].name;

        /** 
         * Similar case here, if the allegiances' list length is 0 
         * then the empty string will be taken down, otherwise the allengiance list for that
         * character will be taken
         */
        if(this.results[i].allegiances.length === 0) this.allegiances[i] = "";
        else this.allegiances[i] = this.results[i].allegiances;

        /**
         * Each individual result is stored in a record with different items for ease of access
         * Currently the allegiance item returns a list with an API
         * A GET request for that API will return the name of the house that the character belongs to
         */
        this.characterName[i] = {
          alias: alias,
          name: name,
          allegiance: this.allegiances[i],
          born: this.results[i].born,
          died: this.results[i].died,
          culture: this.results[i].culture,
          gender: this.results[i].gender
        };
      }

        /**
         * For each character in the list of results, 
         * a GET request is called for the API that is stored in allegiance list
         * the allegiance item in the record is modified with the response as shown below
         */
        for(var i = 0; i < this.characterName.length; i++) {
          await axios
            .get(this.characterName[i].allegiance[0])
            .then(response => {
              this.characterName[i].allegiance = response.data.name;
            })
            .catch(error => {
              console.log(error); // eslint-disable-line no-console
              this.characterName[i].allegiance = "";
            });
        }
      
      // In App.vue, the $emit call starts the searchResponded function with the list of characters as the parameter
      this.$emit('search-responded', this.characterName);
    }
  }
};
</script>

<style scoped>
</style>