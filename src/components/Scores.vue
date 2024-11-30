<template>
  <div class="scores">
    <div id="score-x">X: {{ scores.X }}</div>
    <div id="score-o">O: {{ scores.O }}</div>
  </div>
</template>

<script setup>
defineProps({
  scores: {
    type: Object,
    required: true,
  },
});
</script>

<style lang="css" scoped>
.scores {
  display: flex;
  justify-content: space-between;
  width: 320px;
  margin-top: 20px;
  color: #b8b8d1;
}

.scores div {
  font-size: 1.5rem;
  font-weight: 600;
}

@media (max-width: 480px) {
  .scores div {
    font-size: 1.2rem;
  }
}
</style>
