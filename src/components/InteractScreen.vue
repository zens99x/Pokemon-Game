<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :ref="`card-${index}`"
        :cardsContext="cardsContext"
        :rules="rules"
        @onFlip="checkRule($event)"
      />
    </div>
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
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;

      this.rules.push(card);

      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("dung");

        setTimeout(() => {
          if (
            this.$refs[`card-${this.rules[0].index}`][0] &&
            this.$refs[`card-${this.rules[0].index}`][0].onEnabled
          ) {
            this.$refs[`card-${this.rules[0].index}`][0].onEnabled();
          }
          if (
            this.$refs[`card-${this.rules[1].index}`][0] &&
            this.$refs[`card-${this.rules[1].index}`][0].onEnabled
          ) {
            this.$refs[`card-${this.rules[1].index}`][0].onEnabled();
          }
          this.rules = [];
        }, 1000);

        // Add class disabled to card

        // Reset rules

        const disabledElements = document.querySelectorAll(
          ".screen .card.disabled"
        );
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 800);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("sai");

        setTimeout(() => {
          // Close Card
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();

          // Reset rules
          this.rules = [];
        }, 800);
      } else {
        return false;
      }
    },
  },
};
</script>

<style scoped lang="css">
.screen {
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}

.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
