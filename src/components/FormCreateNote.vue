<template>
  <div class="create-note__form-wrap">
      <transition name="create-note__animation">
        <form v-if="formVisible" class="create-note__form">
          <input
            id="newNoteTitle"
            type="text"
            class="create-note__input create-note__input_title"
            @keyup.enter="addTodo"
            v-model="title"
          />
          <AddNewTodo @add-new-todo="addTodo" />
          <TodoList :todos="this.todos" />
          <div class="btn-group__wrap">
            <button class="btn__create-note btn__create-note_blue" @click.prevent="initNote()">Сохранить</button>
            <button class="btn__create-note btn__create-note_grey" @click.prevent="onCancel()">Отменить</button>
          </div>
          
        </form>
      </transition>
    </div>
</template>

<script>
import AddNewTodo from "@/components/AddNewTodo.vue";
import TodoList from "@/components/TodoList.vue";

export default {
  data() {
    return {
      id: null,
      title: "Введите название заметки",
      todos: [],
    };
  },
  props: {
    formVisible: {
      type: Boolean
    }
  },
  methods: {
    addTodo(todo) {
      if (todo) {
        this.todos.push(todo);
      }
    },
    clearForm(){
      this.id = null;
      this.title = "Введите название заметки";
      this.todos = [];
    },
    initNote(){
      if (this.title.trim()) {
        const note = {
          id: Date.now(),
          title: this.title,
          todos: this.todos
        } 
        this.$emit("init-note", JSON.stringify(note));
        this.clearForm();
      }
    },
    onCancel(){
      this.clearForm();
      this.$emit("hide-form");
    }
  },
  components: {
    TodoList,
    AddNewTodo
  },
}

</script>

<style scoped>

.btn-group__wrap{
  display: flex;
  justify-content: space-between;
}

.btn__create-note {
  margin: 0 0.2rem;
  padding: 10px 25px;
  text-transform: uppercase;
  font-weight: 500;
  border: 0;
  cursor: pointer;
  border-radius: 5px;
}
.btn__create-note:hover,
.btn__create-note:focus {
  border: 0;
  outline: none;
}

.btn__create-note_blue {
  background-color: var(--blue);
  color: #fff;
}
.btn__create-note_blue:hover {
  background-color: #326ff3;
  color: #fff;
}

.btn__create-note_grey {
  background-color: #fff;
  color: var(--secondary-text);
  border: 1px solid var(--secondary-text);
}
.btn__create-note_grey:hover,
.btn__create-note_grey:focus {
  border: 1px solid var(--grey);
  color: var(--grey);
}

.mr-rem-2{
  margin-right: 2rem;
}

.create-note__form-wrap {
  overflow: hidden;
  padding: 15px;
}

.create-note__form {
  width: 100%;
  max-width: 368px;
  min-height: 226px;
  padding: 15px 20px;
  border-radius: 10px;
  background-color: #fff;
  text-align: left;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  -moz-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  margin: 0 auto;
  box-sizing: border-box;
}

.create-note__input {
  display: block;
  width: 100%;
  max-width: 290px;
  padding: 5px 10px;
  margin: 1rem 0;
  color: var(--text);
}

.create-note__input:focus {
  outline: var(--blue);
  color: var(--text);
}

.create-note__input_todo {
  border: 1px solid var(--secondary-blue);
  border-radius: 5px;
}

.create-note__input_title {
  border: 0;
  outline: none;
  border-bottom: 1px solid var(--secondary-blue);
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0.3rem 0 0.5rem;
  padding: 5px 10px;
  color: var(--text);
}

/* Animation */
.create-note__animation-enter-active,
.create-note__animation-leave-active {
  transition: all 0.5s;
}

.create-note__animation-enter,
.create-note__animation-leave-to {
  transform: translateY(-100%);
}
</style>