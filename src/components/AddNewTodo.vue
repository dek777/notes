<template>
  <div class="add-todo__wrap">
    <input
      type="text"
      class="add-todo__input"
      placeholder="Добавить задачу"
      v-model="newTodo"
    />
    <i @click="addTodo" class="flaticon-add icon"></i>
  </div>
</template>

<script>
export default {
  data(){
    return {
      newTodo: ''
    }
  },
  methods: {
    addTodo(){
      if (this.newTodo.trim()) {
        this.$emit('add-new-todo',{
          id: Date.now(),
          text: this.newTodo,
          done: false 
        });
        this.newTodo = "";
      }
    }
  },

};
</script>

<style scoped>

.add-todo__wrap {
  display: flex;
}

.icon {
  color: var(--secondary-blue);
  margin: auto;
}

.icon:hover {
  color: var(--blue);
}

.add-todo__input {
  display: block;
  width: 100%;
  max-width: 290px;
  padding: 5px 10px;
  margin: 1rem 0;
  color: var(--text);
  border: 1px solid var(--secondary-blue);
  border-radius: 5px;
}

.add-todo__input:focus {
  outline: var(--blue);
  color: var(--text);
}

</style>