<script>
import Card from "./Card";
export default {
  components: {
    Card,
  },
  props: {
    cardList: {
      type: Array,
      required: true,
    },
    status: {
      type: String,
      required: true,
    },
    timerCount: {
      type: Number,
      required: true,
    },
    userMoved: {
      type: Number,
      required: true,
    },
  },
  setup(props, ctx) {
    const selectCard = (payload) => {
      ctx.emit("flip-card", payload);
    };
    return {
      selectCard,
    };
  },
};
</script>

<template>
  <transition-group tag="section" class="game-board" name="shuffle-card">
    <Card
      v-for="card in cardList"
      :key="`${card.value}-${card.variant}`"
      :matched="card.matched"
      :value="card.value"
      :visible="card.visible"
      :position="card.position"
      @select-card="selectCard"
    />
  </transition-group>
  <h2 class="status">Time Remainig :{{ timerCount }}</h2>
  <h2 class="status">Remained Moves: {{ userMoved }}</h2>
</template>

<style>
* {
  color: black !important;
}
</style>
