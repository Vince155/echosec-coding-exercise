<template>
  <v-app>
    <v-toolbar app>
      <search-bar-input/>
    </v-toolbar>
    <v-content>
      <results
        :results="results"
      />
    </v-content>
  </v-app>
</template>

<script>
import SearchBarInput from './components/SearchBarInput';
import Results from './components/Results';

export default {
  name: 'App',
  components: {
    SearchBarInput,
    Results,
  },
  data: () => ({
    results: [
      '1',
      '2',
      '3',
    ],
  })
};
</script>
