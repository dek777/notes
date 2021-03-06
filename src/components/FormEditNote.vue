<template>
  <div class="edit-note__form-wrap">

    <!-- Control buttons -->
    <UndoRedo
      :length="statesStack.length"
      :counter="currentStateIndex"
      @undo="undo"
      @redo="redo"
      @discard-changes="showhideDiscardModalVisible"
      @remove="showhideDeleteModalVisible"
    />
    <!-- Modals -->
    <ConfirmModal :confirmModalVisible="confirmDeleteModalVisible" @confirm="deleteNote" @cancel="showhideDeleteModalVisible">Вы уверены, что хотите удалить заметку?</ConfirmModal>
    <ConfirmModal :confirmModalVisible="confirmDiscardModalVisible" @confirm="discardChanges" @cancel="showhideDiscardModalVisible">Вы уверены, что хотите отменить все изменения?</ConfirmModal>

    <!-- Note Editing Form-->
    <form class="edit-note__form">
      <EditTitleNote
        :text="statesStack[currentStateIndex].title"
        @change-title="changeTitle"
      />
      <AddNewTodo @add-new-todo="addTodo" />
      <TodoList
        :todos="statesStack[currentStateIndex].todos"
        @delete-todo="deleteTodo"
        @done-undone-todo="doneUndoneTodo"
      />
      <div class="btn-group__wrap">
        <button class="btn btn_blue" @click.prevent="saveNote()">
          Сохранить
        </button>
        <button class="btn btn_grey" @click.prevent="onCancel()">
          Отменить
        </button>
      </div>
    </form>

  </div>
</template>

<script>
import AddNewTodo from "@/components/AddNewTodo.vue";
import TodoList from "@/components/TodoList.vue";
import EditTitleNote from "@/components/EditTitleNote.vue";
import UndoRedo from "@/components/UndoRedo.vue";
import ConfirmModal from "@/components/ConfirmModal.vue";

export default {
  data() {
    return {
      statesStack: [], //массив состояний заметки для undo-redo
      currentStateIndex: 0, //индекс текущего состояния заметки в массиве состояний statesStack
      confirmDeleteModalVisible: false,
      confirmDiscardModalVisible: false,
    };
  },
  props: {
    note: {
      type: [Object, Array],
    },
  },
  computed: {
    originNote: (thisComponent) => JSON.stringify(thisComponent.note), //убираем реактивность (заметка до всех изменений - оригинал)
  },
  methods: {
    initNextStateNote() {
      //если индекс текущего состояния заметки меньше длины массива состояний 
      //(добавление нового состояния заметки после нажатий undo), все состояния после текущего индекса удаляем (redo становится неактивна)
      if (this.currentStateIndex < this.statesStack.length - 1) {
        this.statesStack = this.statesStack.splice(0, this.currentStateIndex + 1);
      }
      //сохраняем текущее состояние заметки в statesStack и увеличиваем индекс
      this.statesStack.push(this.statesStack[this.currentStateIndex]);
      this.statesStack[this.currentStateIndex] = JSON.parse(
        JSON.stringify(this.statesStack[this.currentStateIndex])
      );
      this.currentStateIndex++;
    },
    addTodo(todo) {
      if (todo) {
        this.initNextStateNote();
        this.statesStack[this.currentStateIndex].todos.push(todo);
      }
    },
    deleteTodo(id) {
      if (id) {
        this.initNextStateNote();
        this.statesStack[this.currentStateIndex].todos = this.statesStack[
          this.currentStateIndex
        ].todos.filter((todo) => todo.id !== id);
      }
    },
    changeTitle(newTitle) {
      this.initNextStateNote();
      this.statesStack[this.currentStateIndex].title = newTitle;
    },
    doneUndoneTodo(todo) {
      this.initNextStateNote();
      todo.done = !todo.done;
    },
    clearForm() {
      this.statesStack = [];
    },
    showhideDeleteModalVisible(){
      this.confirmDeleteModalVisible = !this.confirmDeleteModalVisible;
    },
    showhideDiscardModalVisible(){
      this.confirmDiscardModalVisible = !this.confirmDiscardModalVisible;
    },
    undo() {
      this.currentStateIndex--;
    },
    redo() {
      this.currentStateIndex++;
    },
    discardChanges(){
      this.statesStack = this.statesStack.splice(0, 1);
      this.currentStateIndex = 0;
    },
    deleteNote(){
      this.$emit('delete-note', this.note.id);
    },
    saveNote() {
      this.$emit('save-note', this.note, this.statesStack[this.currentStateIndex]);
    },
    onCancel() {
      this.$router.push('/');
    },
  },
  components: {
    TodoList,
    AddNewTodo,
    EditTitleNote,
    UndoRedo,
    ConfirmModal
  },
  created: function () {
    this.statesStack.push(JSON.parse(this.originNote));
  },
};
</script>

<style scoped>
.btn-group__wrap {
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

.mr-rem-2 {
  margin-right: 2rem;
}

.edit-note__form-wrap {
  overflow: hidden;
  padding: 0 15px 15px;
}

.edit-note__form {
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

.icon {
  color: var(--secondary-blue);
  margin: auto;
}

.icon:hover {
  color: var(--blue);
}
</style>