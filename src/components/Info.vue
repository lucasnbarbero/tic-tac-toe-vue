<template>
  <div class="info">
    <p id="turn-indicator">
      <template v-if="winner">
        {{ winner === "Empate" ? "Empate" : `Ganador: ${winner}` }}
      </template>
      <template v-else> Turno de: {{ turn }} </template>
    </p>
  </div>
</template>

<script setup>
defineProps({
  turn: {
    type: String,
    required: true,
  },
  winner: {
    type: String,
    default: null,
  },
});
</script>

<style lang="css" scoped>
.info {
  margin-bottom: 20px;
  text-align: center;
}

.info p {
  font-size: 1.5rem;
  color: #b8b8d1;
}
</style>
