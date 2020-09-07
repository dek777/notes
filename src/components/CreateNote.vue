<template>
  <div class>
    <button class="btn__create-note" @click.prevent="showHideForm">Новая заметка</button>
    <div class="create-note__form-wrap">
      <transition name="create-note__animation">
        <form v-if="formVisible" class="create-note__form">
          <input
            type="text"
            class="create-note__input create-note__input_title"
            value="Введите название заметки"
          />
          <div class="create-note__add-todo-wrap">
            <input
              type="text"
              class="create-note__input create-note__input_todo"
              placeholder="Добавить задачу"
            />
            <i class="flaticon-add icon"></i>
          </div>
        </form>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formVisible: false,
    };
  },
  methods: {
    showHideForm() {
      this.formVisible = !this.formVisible;
    },
  },
};
</script>

<style scoped>
.btn__create-note {
  margin: 2rem auto;
  padding: 15px 25px;
  background-color: var(--blue);
  color: #fff;
  text-transform: uppercase;
  font-weight: 600;
  border: 0;
  cursor: pointer;
  border-radius: 5px;
}
.btn__create-note:hover,
.btn__create-note:focus {
  border: 0;
  outline: none;
}
.btn__create-note:hover {
  background-color: #326ff3;
  color: #fff;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  -moz-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
}

.create-note__form-wrap {
  overflow: hidden;
  padding: 15px;
}

.create-note__form {
  width: 100%;
  max-width: 378px;
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
  margin: 0.3rem 0 1.5rem;
  padding: 5px 10px;
  color: var(--text);
}

.create-note__add-todo-wrap{
  display: flex;
}

.icon {
    color: var(--secondary-blue);
    margin: auto;
}

.icon:hover {
    color: var(--blue);
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