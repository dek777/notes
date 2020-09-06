<template>
  <div class="todos__wrap">
    <TodoItem v-for="(todo, i) in todos" :key="i" :todo="todo" :index="i"/>
  </div>
</template>

<script>

import TodoItem from '@/components/TodoItem.vue'

export default {
  props: {
    todos: {
      type: [Object, Array],
      required: true
    }
  },
  components: {
    TodoItem
  }
}
</script>

<style scoped>

</style>