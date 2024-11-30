<template>
  <h1>Tic Tac Toe</h1>
  <Info :turn="turn" :winner="winner" />
  <Grid
    :cells="cells"
    :winner="winner"
    :winning-cells="winningCells"
    @cell-click="handleCellClick"
  />
  <Scores :scores="scores" />
</template>

<script setup>
import { ref } from "vue";

import Grid from "./components/Grid.vue";
import Info from "./components/Info.vue";
import Scores from "./components/Scores.vue";

const turns = { X: "O", O: "X" };
const turn = ref("X");
const cells = ref(Array(9).fill(null));
const scores = ref({ X: 0, O: 0 });
const winner = ref(null);
const winningCells = ref([]);

const winningCombinations = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8],
  [0, 4, 8],
  [2, 4, 6],
];

function toggleTurn() {
  turn.value = turns[turn.value];
}

function handleCellClick(index) {
  if (cells.value[index] || winner.value) return;

  cells.value[index] = turn.value;

  if (checkWinner()) {
    scores.value[turn.value]++;
    winner.value = turn.value;
    setTimeout(resetGame, 2000);
    return;
  }

  if (!cells.value.includes(null)) {
    winner.value = "Empate";
    setTimeout(resetGame, 2000);
    return;
  }

  toggleTurn();
}

function checkWinner() {
  for (let [a, b, c] of winningCombinations) {
    if (
      cells.value[a] &&
      cells.value[a] === cells.value[b] &&
      cells.value[a] === cells.value[c]
    ) {
      winningCells.value = [a, b, c];
      return true;
    }
  }
  return false;
}

function resetGame() {
  cells.value.fill(null);
  winner.value = null;
  winningCells.value = [];
  turn.value = "X";
}
</script>

<style lang="css" scoped>
h1 {
  font-size: 3rem;
  font-weight: 600;
  margin-bottom: 20px;
  color: #ffde59;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4);
  text-align: center;
}

@media (max-width: 480px) {
  h1 {
    font-size: 2.5rem;
  }
}
</style>
