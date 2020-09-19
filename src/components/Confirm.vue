<template>
  <div class="confirm__overflow_hidden">
    <transition name="confirm__animation">
      <div v-if="confirmBlockVisible" class="confirm__wrap">
        <p class="confirm__text">Удалить?</p>
        <div class="confirm__btn-group">
          <button class="confirm__btn confirm__btn_yes" @click.prevent="deleteItem">Да</button>
          <button class="confirm__btn confirm__btn_no" @click.prevent="cancel">Нет</button>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    confirmBlockVisible: {
      type: Boolean,
    },
  },
  methods: {
    deleteItem() {
      this.$emit("cancel");
      setTimeout( () => this.$emit("confirm"), 500 );
    },
    cancel() {
      this.$emit("cancel");
    },
    
  },
};
</script>

<style scoped>
* { 
  box-sizing: border-box;
}

.confirm__overflow_hidden{
  overflow-y: hidden;
}

.confirm__wrap {
  background-color: var(--blue);
  color: #fff;
  display: flex;
  justify-content: space-between;
  padding: 10px 15px;
  border-radius: 5px;
  margin-bottom: 1rem;
}

.confirm__text {
  font-size: 0.9rem;
  margin: auto 0;
}

.confirm__btn-group {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  margin: auto 0;
}

.confirm__btn {
  padding: 3px 15px;
  font-weight: 500;
  font-size: 0.9rem;
  cursor: pointer;
  border-radius: 5px;
  max-height: 30px;
}

.confirm__btn:hover,
.confirm__btn:focus {
  outline: none;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3); /*rgba(50, 50, 50, 0.3);*/
  -moz-box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3);
  box-shadow: 0px 5px 10px 0px rgba(147, 175, 236, 0.3);
}

.confirm__btn_yes {
  background-color: #fff;
  color: var(--blue);
  border: 1px solid #fff;
}

.confirm__btn_no {
  background-color: var(--blue);
  color: #fff;
  border: 1px solid #fff;
}

/* Animation */
.confirm__animation-enter-active,
.confirm__animation-leave-active {
  transition: all 0.5s;
}

.confirm__animation-enter,
.confirm__animation-leave-to {
  transform: translateY(-100%);
}
</style>