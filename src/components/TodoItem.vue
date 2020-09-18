<template>
  <div class="todo__wrap">
    <p class="todo__text">
      <span class="todo__index">{{ index + 1 }}</span>
      {{ todo.text }}
    </p>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: [Object, Array],
      required: true,
    },
    index: {
      type: Number,
    },
  },
  components: {},
};
</script>

<style scoped>
.todo__text {
  font-size: 1.001rem;
  margin: 0.5rem 0;
}
.todo__index {
  margin-right: 1rem;
  display: inline-block;
  font-weight: 500;
  text-align: center;
  color: #fff;
  width: 25px;
  background-color: #4279ee;
  border-radius: 50%;
  height: 25px;
  line-height: 25px;
}
</style>