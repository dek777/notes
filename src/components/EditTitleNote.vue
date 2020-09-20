<template>
  <div class="">
    <input
      type="text"
      class="edit-title__input edit-title__input_title"
      :class="{input_error : isTitleEmpty}"
      placeholder="Введите название заметки"
      @change="titleChange"
      @blur="onUnfocus"
      ref="inputTitle"
      v-model="newTitle"
    />
    <transition name="error-animation">
      <div v-if="isTitleEmpty" class="error__wrap">
        <p class="error__text">Введите название заметки</p>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isTitleEmpty: false,
      newTitle: ''
    }
  },
  props: {
    text: {
      type: String
    }
  },
  created: 
    function(){
      this.newTitle = JSON.parse(JSON.stringify(this.text));
    }
  ,
  methods: {
    onUnfocus(){
      if (!this.$refs['inputTitle'].value){
        this.isTitleEmpty = true;
      }
    },
    titleChange(){
      if (this.newTitle.trim()){
        this.isTitleEmpty = false;
        this.$emit("change-title", this.newTitle)
      } else {
        this.isTitleEmpty = true;
      }
    }
  },
  
}
</script>

<style scoped>

.edit-title__input {
  display: block;
  width: 100%;
  max-width: 290px;
  padding: 5px 10px;
  margin: 1rem 0;
  color: var(--text);
}

.edit-title__input:focus {
  outline: var(--blue);
  color: var(--text);
}

.edit-title__input_todo {
  border: 1px solid var(--secondary-blue);
  border-radius: 5px;
}

.edit-title__input_title {
  border: 0;
  outline: none;
  border-bottom: 1px solid var(--secondary-blue);
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0.3rem 0 0.5rem;
  padding: 5px 10px;
  color: var(--text);
}

.input_error{
  border-bottom: 2px solid var(--error-color);
}

/* Error */
.error__wrap{
  overflow: hidden;
}

.error__text{
  font-size: 0.8rem;
  color: var(--error-color);
  font-weight: 600;
  padding: 0 10px;
  margin-top: 0;
}

/* Animation */
.error-animation-enter-active,
.error-animation-leave-active {
  transition: all 0.5s;
}

.error-animation-enter,
.error-animation-leave-to {
  transform: translateY(-100%);
}


</style>