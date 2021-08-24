<template>
  <h1>Memory Game</h1>
  <div class="board">
    <Card
      v-for="(card, index) in cardsList"
      :key="`card-${index}`"
      :visible="card.visible"
      :value="card.value"
      :position="card.position"
      @select-card="flipCard"
    />
  </div>
</template>

<script>
import { ref } from "vue";
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Card,
  },

  setup() {
    const cardsList = ref([]);

    for (let i = 0; i < 16; i++) {
      cardsList.value.push({
        value: i,
        visible: false,
        position: i,
      });
    }

    const flipCard = (payload) => {
      cardsList.value[payload.position].visible = true;
    };
    return {
      cardsList,
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
