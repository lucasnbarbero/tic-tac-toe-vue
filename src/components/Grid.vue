<template>
  <div class="grid">
    <div
      v-for="(content, index) in cells"
      :key="index"
      class="cell"
      role="button"
      aria-label="Casilla vacía"
      :class="{ winner: winningCells.includes(index) }"
      @click="() => $emit('cell-click', index)"
    >
      {{ content }}
    </div>
  </div>
</template>

<script setup>
defineProps({
  cells: {
    type: Array,
    required: true,
  },
  winner: {
    type: String,
    default: null,
  },
  winningCells: {
    type: Array,
    default: () => [],
  },
});
</script>

<style lang="css" scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(3, auto);
  gap: 10px;
  margin: 20px 0;
}

.cell {
  width: 100px;
  height: 100px;
  background-color: #292940;
  border: 2px solid #3f3f5e;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2.5rem;
  font-weight: bold;
  color: #ffde59;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s, box-shadow 0.3s;
}

.cell:hover {
  background-color: #39395a;
  transform: scale(1.1);
  box-sizing: 0 4px 10px rgba(0, 0, 0, 0.4);
}

.winner {
  background-color: #6ea8d4 !important; /* Azul suave */
  color: #ffffff;
  animation: blink 1s ease-in-out infinite alternate;
}

@keyframes blink {
  from {
    box-shadow: 0 0 10px rgba(110, 168, 212, 0.7); /* Azul claro */
  }
  to {
    box-shadow: 0 0 20px rgba(110, 168, 212, 1); /* Azul un poco más intenso */
  }
}

@media (max-width: 480px) {
  .grid {
    grid-template-columns: repeat(3, 80px);
    gap: 8px;
  }

  .cell {
    width: 80px;
    height: 80px;
    font-size: 2rem;
  }
}
</style>
