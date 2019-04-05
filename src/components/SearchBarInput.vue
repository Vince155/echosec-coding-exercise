<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm6>
      <v-text-field
        label="Search"
        single-line
        solo
        prepend-inner-icon="search"
        clearable
      ></v-text-field>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    name: 'SearchBarInput',
  };
</script>

<style scoped>

</style>