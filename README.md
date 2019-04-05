# Echosec Coding Exercise

This is a pre-interview coding exercise for the Echosec development team. As an Echosec developer You will be responsible for developing and maintaining features and data-sets for the Echosec open data search and aggregation products.

Echosec Search is a search and alerting tool for location-based social media. We provide an easy to use interface for open data analysists, security experts, journalists to find up to date crowdsourced information about real-world events.

Beacon sheds light on the dark web by combining indexes of TOR sites, paste-bin dumps, public discord and telegram chat logs into an advanced search interface for cybersecurity professionals.

We value a curious attitude towards discovering and delivering new open source data to our end customers. The purpose of the exercise is to create a common framework that utilizes many of the same patterns we use in our production applications to discuss during your technical interview. We encourage you to take this project in a direction that compels you. Expand and share your work on this however you like.

## Task

Using the [API of Ice and Fire](https://anapioficeandfire.com/Documentation), create a Vue.js application that allows users to search for A Song of Ice and Fire characters and display them within the application.

There are a number of comments within the code base labeled `EXERCISE` which are left up to the developer to implmeent.

We recomend first implementing the search functionality in `SearchBarInput.vue` and then working your way through `App.vue` and `Results.vue`.

## Requirements

- Typing a character name in the search bar should show all results for that character.
- If the user hits enter with no character name, all results should be displayed from the API response.
- Display the name, alias, gender, culture, date of birth, date of death (if present), and allegiances for each character returned.
- How you style the application is entirely up to you. You may either use Vuetify or custom CSS.

## Development Box

A recent version of node.js is required. The coding example was tested and run on `v10.13.0`.

To install the dependencies run `npm install`.

You can then run `npm run serve` to re-compile your changes in real time or `npm run build` to see the changes after the fact.

## Resources

- API of Ice and Fire: https://anapioficeandfire.com/Documentation#characters
- Axios documentation: https://github.com/axios/axios
- Vuetify documentation: https://vuetifyjs.com/en/components/api-explorer
- Vue.js documentation: https://vuejs.org/v2/guide/


## Steps

- Fork the repository
- Clone the forked git repo to your local environment
- Install dependencies using `npm install`
- Compile code using `npm run serve` or `npm run build`
- Display results upon searching
- Comment your code
- Push your code to github
- Submit a pull request when done
