<template>
  <div>
    <transition name="bg-fade-animate">
      <div v-if="confirmModalVisible" class="confirm__bg" @click="onClickOutModal">
        <div class="confirm__modal">
          <p class="question_circle">?</p>
          <p class="confirm__text">Вы уверены, что хотите удалить заметку?</p>
          <div class="confirm__btn-group">
            <button class="confirm__btn confirm__btn_yes" @click.prevent="deleteItem">Да</button>
            <button class="confirm__btn confirm__btn_no" @click.prevent="cancel">Нет</button>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    confirmModalVisible: {
      type: Boolean,
    },
  },
  methods: {
    deleteItem() {
      this.$emit("delete-item");
    },
    cancel() {
      this.$emit("cancel");
    },
    onClickOutModal(event) {
      if (!event.target.closest(".confirm__modal")) {
        this.$emit("cancel");
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.confirm__bg {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7); /*rgba(66, 121, 238, 0.4);*/
  z-index: 10;
  display: flex;
  padding: 15px;
  box-sizing: border-box;
}

.confirm__modal {
  background-color: #fff;
  color: var(--text);
  padding: 0 25px 25px;
  border-radius: 5px;
  margin: auto;
  min-width: 250px;
  max-width: 330px;
}

.confirm__text {
  font-size: 0.9rem;
  margin: 2rem 0;
}

.question_circle {
  font-size: 2.5rem;
  width: max-content;
  margin: 1rem auto;
  color: #fff;
  background-color: var(--blue);
  padding: 0.2rem 1rem;
  border-radius: 50%;
  text-align: center;
}

.confirm__btn-group {
  display: flex;
  justify-content: flex-end;
  margin: auto 0;
}

.confirm__btn {
  padding: 7px 20px;
  font-weight: 500;
  font-size: 0.9rem;
  cursor: pointer;
  border-radius: 5px;
  width: 100%;
}

.confirm__btn:hover,
.confirm__btn:focus {
  outline: none;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3); /*rgba(50, 50, 50, 0.3);*/
  -moz-box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3);
  box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3);
}

.confirm__btn_yes {
  background-color: var(--blue);
  color: #fff;
  border: 1px solid var(--blue);
  margin-right: 0.8rem;
}

.confirm__btn_no {
  background-color: #fff;
  color: var(--blue);
  border: 1px solid var(--blue);
}

/* Animation */

.bg-fade-animate-enter-active,
.bg-fade-animate-leave-active {
  transition: opacity 0.5s;
}

.bg-fade-animate-enter,
.bg-fade-animate-leave-to {
  opacity: 0;
}

@keyframes modal-animation {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(0);
  }
}
</style>