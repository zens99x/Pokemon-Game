<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
    />
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },
};
</script>

<style></style>
