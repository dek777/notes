<template>
  <div class="todo_totals">
    <p v-if="todosCount" class="totals__text">Всего задач: {{ todosCount }}</p>
    <p v-else class="totals__text totals__text_empty">Список задач пуст</p>
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

.totals__text_empty{
  bottom: 15px;
  top: 40%;
  left: 0;
  right: 0;
  text-align: center;
}

</style>