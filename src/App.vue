<template>
  <h1>Memory Game</h1>
  <div class="board">
    <Card
      v-for="(card, index) in cardsList"
      :key="`card-${index}`"
      :matched="card.matched"
      :visible="card.visible"
      :value="card.value"
      :position="card.position"
      @select-card="flipCard"
    />
  </div>
  <h2>{{ status }}</h2>
</template>

<script>
import { ref, watch } from "vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Card,
  },

  setup() {
    const cardsList = ref([]);
    const userSelection = ref([]);
    const status = ref("");

    for (let i = 0; i < 16; i++) {
      cardsList.value.push({
        value: i,
        visible: false,
        position: i,
        matched: false,
      });
    }

    const flipCard = (payload) => {
      cardsList.value[payload.position].visible = true;

      if (userSelection.value[0]) {
        userSelection.value[1] = payload;
      } else {
        userSelection.value[0] = payload;
      }
    };
    watch(
      userSelection,
      (currentValue) => {
        if (currentValue.length === 2) {
          const cardOne = currentValue[0];
          const cardTwo = currentValue[1];

          if (cardOne.faceValue === cardTwo.faceValue) {
            status.value = "Matched";

            cardsList.value[cardOne.position] = true;
            cardsList.value[cardTwo.position] = true;
          } else {
            status.value = "Mismatch";
            cardsList.value[cardOne.position].visible = false;
            cardsList.value[cardTwo.position].visible = false;
          }

          userSelection.value.length = 0;
        }
      },
      { deep: true }
    );

    return {
      cardsList,
      userSelection,
      status,
      flipCard,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.board {
  display: grid;
  grid-template-columns: 150px 150px 150px 150px;
  grid-template-rows: 150px 150px 150px 150px;
  grid-column-gap: 20px;
  grid-row-gap: 20px;
  align-items: center;
  justify-content: center;
}
</style>
