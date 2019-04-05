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
  export default {
    name: 'SearchBarInput',
    data: () => ({
      searchInput: '',
    }),
    methods: {
      submitSearch() {

      },
    },
  };
</script>

<style scoped>

</style>