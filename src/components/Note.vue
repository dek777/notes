<template>
  <div class="note__card">
    <div class="note__title-wrap">
      <p class="note__title">{{note.title}}</p>
      <div class="icons__wrap">
        <i class="flaticon-pencil icon"></i>
        <i class="flaticon-delete icon"></i>
      </div>
    </div>

    <TodoList :todos="note.todos" />
    <TodoTotals :todosCount="note.todos.length" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoTotals from "@/components/TodoTotals.vue";

export default {
  props: {
    note: {
      type: [Object, Array],
      required: true,
    },
  },
  components: {
    TodoList,
    TodoTotals,
  },
};
</script>

<style scoped>
.note__card {
  padding: 15px 20px;
  border-radius: 10px;
  background-color: #fff;
  text-align: left;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  -moz-box-shadow:    0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  box-shadow:         0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  position: relative;
}

.note__title {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0.3rem 0 1.5rem;
}

.note__title-wrap {
  display: flex;
  justify-content: space-between;
}

.icons__wrap{
  padding: 5px;
}
</style>