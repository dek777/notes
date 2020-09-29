<template>
  <div class>
    <div v-if="!isEditPage" class="todos__wrap">
      <TodoItem v-for="(todo, i) in todosSliced" :key="i" :todo="todo" :index="i" />
    </div>
    <div v-if="isEditPage" class="todos__wrap">
      <p v-if="!todos.length" class="text__empty-list">Список задач пуст</p>
      <TodoItemEdit v-for="(todo, i) in todos" :key="i" :todo="todo" :index="i" @delete-todo="deleteTodo" @done-undone-todo="doneUndoneTodo" />
    </div>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
import TodoItemEdit from "@/components/TodoItemEdit.vue";

export default {
  props: {
    todos: {
      type: [Object, Array],
      required: true,
    },
    maxTodosCount: { //количество задач при выводе заметки 
      type: Number,
      default: 3
    }
  },
  components: {
    TodoItem,
    TodoItemEdit
  },
  computed: {
    isEditPage: (thisComponent) =>
      thisComponent.$route.name === "EditPage" ? true : false,
    todosSliced: function () {
      return this.todos.slice(0,this.maxTodosCount)
    }
  },
  methods: {
    deleteTodo(id) {
      this.$emit('delete-todo', id);
    },
    doneUndoneTodo(todo) {
      this.$emit('done-undone-todo', todo);
    },
  }
};
</script>

<style scoped>
.todos__wrap {
  margin-bottom: 3rem;
}

.text__empty-list{
  text-align: center;
  font-size: 0.9rem;
  color: var(--secondary-text);
}
</style>