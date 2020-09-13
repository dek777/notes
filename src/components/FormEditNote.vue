<template>
  <div class="create-note__form-wrap">
        <form class="create-note__form">
          <input
            id="newNoteTitle"
            type="text"
            class="create-note__input create-note__input_title"
            v-model="title"
          />
          <div class="create-note__add-todo-wrap">
            <input
              type="text"
              class="create-note__input create-note__input_todo"
              placeholder="Добавить задачу"
              v-model="newTodo"
            />
            <i @click="addTodo" class="flaticon-add icon"></i>
          </div>
          <TodoList :todos="this.todos" />
          <div class="btn-group__wrap">
            <button class="btn btn_blue" @click.prevent="initNote()">Сохранить</button>
            <button class="btn btn_grey" @click.prevent="onCancel()">Отменить</button>
          </div>
          
        </form>
    </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";

export default {
  data() {
    return {
      id: this.note.id,
      title: this.note.title,
      todos: this.note.todos,
      newTodo: "",
    };
  },
  props: {
    note: {
      type: [Object, Array]
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          id: Date.now(),
          text: this.newTodo,
        });
        this.newTodo = "";
      }
    },
    clearForm(){
      this.id = null;
      this.title = "Введите название заметки";
      this.todos = [];
      this.newTodo = "";
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
  },
}

</script>

<style scoped>

.btn-group__wrap{
  display: flex;
  justify-content: space-between;
}

.btn {
  margin: 0 0.2rem;
  padding: 10px 25px;
  text-transform: uppercase;
  font-weight: 500;
  border: 0;
  cursor: pointer;
  border-radius: 5px;
  width: 100%;
}
.btn:hover,
.btn:focus {
  border: 0;
  outline: none;
}

.btn_blue {
  background-color: var(--blue);
  color: #fff;
  margin-right: 1rem;
}
.btn_blue:hover {
  background-color: #326ff3;
  color: #fff;
}

.btn_grey {
  background-color: #fff;
  color: var(--secondary-text);
  border: 1px solid var(--secondary-text);
}
.btn_grey:hover,
.btn_grey:focus {
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

.create-note__add-todo-wrap {
  display: flex;
}

.icon {
  color: var(--secondary-blue);
  margin: auto;
}

.icon:hover {
  color: var(--blue);
}


</style>