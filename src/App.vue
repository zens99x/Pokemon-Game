<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
  />
  <!-- <result-screen />
  <copy-right-screen /> -->
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
// import CopyRightScreen from "./components/CopyRightScreen.vue";
// import ResultScreen from "./components/ResultScreen.vue";

import { shuffled } from "./utils/array";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running,", config);
      this.settings.totalOfBlocks = config.totalOfBlocks;

      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );

      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];

      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );

      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
  },
  components: {
    MainScreen,
    InteractScreen,
    // CopyRightScreen,
    // ResultScreen,
  },
};
</script>

<style></style>
