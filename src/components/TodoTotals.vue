<template>
  <div class="todo_totals">
    <p class="totals__text">Всего задач: {{ todosCount }}</p>
  </div>
</template>

<script>
export default {
  props: {
    todosCount: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.totals__text {
  margin: 1.5rem 0 0;
  font-size: 0.9rem;
  color: var(--secondary-text);
  position: absolute;
  bottom: 15px;
}
</style>