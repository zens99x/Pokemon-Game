<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen v-if="statusMatch === 'match'" />
  <!-- <result-screen />
  <copy-right-screen /> -->
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
// import CopyRightScreen from "./components/CopyRightScreen.vue";
// import ResultScreen from "./components/ResultScreen.vue";

export default {
  name: "App",
  data() {
    return {
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      console.log("running,", config);
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
