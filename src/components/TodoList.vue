<template>
  <div class>
    <div v-if="!isEditPage" class="todos__wrap">
      <TodoItem v-for="(todo, i) in todos" :key="i" :todo="todo" :index="i" />
    </div>
    <div v-if="isEditPage" class="todos__wrap">
      <TodoItemEdit v-for="(todo, i) in todos" :key="i" :todo="todo" :index="i" />
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
  },
  components: {
    TodoItem,
    TodoItemEdit
  },
  computed: {
    isEditPage: (vueInstance) =>
      vueInstance.$route.name === "EditPage" ? true : false,
  },
};
</script>

<style scoped>
.todos__wrap {
  margin-bottom: 3rem;
}
</style>