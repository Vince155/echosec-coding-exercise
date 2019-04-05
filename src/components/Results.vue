<template>
  <v-layout justify-center>
    <v-flex xs12 sm6>
      <v-card
        v-for="(result, index) in results"
        :key="index"
        height="100"
        class="ma-3 pa-3"
      >
        {{ result }}
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  export default {
    name: 'Results',
    props: {
      results: {
        type: Array,
        required: true,
      },
    },
  };
</script>

<style scoped>

</style>
