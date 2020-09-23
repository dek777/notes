<template>
  <div class>
    <div class="todo__text-wrap">
      <span class="todo__checkbox" @click="doneUndoneTodo"></span>
      <span v-if="todo.done" class="todo__checkbox_checked">&#10004;</span>
      <!-- <input type="text" class="todo__input" v-model="todo.text" /> -->
      <p v-show="!todoEditMode" class="todo__text-field" @click="toggleTodoEditMode">{{todo.text}}</p>
      <!-- <div contenteditable="true" class="todo__input" @blur="deleteTodo" @keyup.enter="deleteTodo">{{todo.text}}</div> -->
      <textarea
        v-show="todoEditMode"
        class="todo__text-field todo__textarea"
        @blur="toggleTodoEditMode"
        @keyup.enter="toggleTodoEditMode"
        ref="todoTextarea"
        @focus="autoresize"
        @keyup="autoresize"
        v-model="todo.text"
      ></textarea>
      <i class="flaticon-delete remove-icon" @click="showHideConfirmBlock"></i>
    </div>
    <Confirm
      :confirmBlockVisible="confirmBlockVisible"
      @confirm="deleteTodo"
      @cancel="showHideConfirmBlock"
    />
  </div>
</template>

<script>
import Confirm from "@/components/Confirm.vue";

export default {
  data() {
    return {
      confirmBlockVisible: false,
      todoEditMode: false, //режим редактирования текста todo
    };
  },
  props: {
    todo: {
      type: [Object, Array],
      required: true,
    },
  },
  components: {
    Confirm,
  },
  methods: {
    doneUndoneTodo() {
      //чекбокс для todo (выполнено - не выполнено)
      //this.todo.done = !this.todo.done;
      this.$emit('done-undone-todo',this.todo);
    },
    showHideConfirmBlock() {
      //открыть-скрыть блок подтверждения
      this.confirmBlockVisible = !this.confirmBlockVisible;
    },
    toggleTodoEditMode() {
      //переключаем режим редактирования todo
      this.todoEditMode = !this.todoEditMode;
      if (this.todoEditMode) {
        this.$nextTick(() => {
          this.$refs.todoTextarea.focus();
        });
      }
    },
    deleteTodo() {
      this.$emit('delete-todo',this.todo.id);
    },
    autoresize(event) {
      const textarea = event.target;
      textarea.style.cssText = "height:" + textarea.scrollHeight + "px";
    },
  },
};
</script>

<style scoped>
.todo__text-wrap {
  font-size: 1.001rem;
  margin: 0.5rem 0;
  position: relative;
  display: flex;
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

.todo__checkbox {
  width: 18px;
  height: 18px;
  border: 1px solid var(--secondary-blue);
  position: absolute;
  cursor: pointer;
  z-index: 2;
}

.todo__checkbox:hover {
  -webkit-box-shadow: 0px -2px 10px 0px rgba(66, 121, 238, 0.4);
  -moz-box-shadow: 0px -2px 10px 0px rgba(66, 121, 238, 0.4);
  box-shadow: 0px -2px 10px 0px rgba(66, 121, 238, 0.4);
}

.todo__checkbox_checked {
  position: absolute;
  color: var(--blue);
  font-size: 19px;
  top: -5px;
  left: 1px;
  cursor: pointer;
  z-index: 1;
}

.todo__text {
  padding-left: 30px;
}

.todo__text-field {
  color: var(--text);
  width: 100%;
  margin: 0 30px;
  border: 0;
  font-size: 1rem;
  box-sizing: border-box;
  border-bottom: 1px solid #fff;
  line-height: 1.4;
  /* word-break: break-all;  перенос слов*/
}

.todo__text-field:hover,
.todo__text-field:focus {
  border: 0;
  outline: none;
  border-bottom: 1px solid var(--secondary-blue);
}

.todo__textarea {
  resize: none;
  height: auto;
  overflow: hidden;
  font-family: "Gilroy", sans-serif;
  padding: 0;
}

.remove-icon {
  color: var(--secondary-blue);
  cursor: pointer;
  position: absolute;
  right: 0;
}

.remove-icon:hover {
  color: var(--blue);
}
</style>