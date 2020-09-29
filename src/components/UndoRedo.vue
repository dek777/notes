<template>
  <div class="undoredo__wrap">
    <button :disabled="isUndoBtnDisabled" class="undoredo__btn" @click.prevent="undo"><i class="flaticon-back-arrow undoredo__icon"></i></button>
    <button :disabled="isRedoBtnDisabled" class="undoredo__btn" @click.prevent="redo"><i class="flaticon-redo-arrow undoredo__icon"></i></button>
    <button :disabled="isDiscardBtnDisabled" class="undoredo__btn" @click.prevent="discardChanges"><i class="flaticon-signal undoredo__icon"></i></button>
    <button class="undoredo__btn" @click.prevent="remove"><i class="flaticon-delete undoredo__icon"></i></button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isUndoBtnDisabled: false, //
      isRedoBtnDisabled: false,
      isDiscardBtnDisabled: false
    }
  },
  props: {
    length: {
      type: Number
    },
    counter: {
      type: Number
    }
  },
  watch: {
    counter: function() {
      this.validate();
    },
  },
  mounted: [
    function(){
      this.validate();
    },
  ],
    
  methods: {
    undo(){
      this.$emit("undo");
    },
    redo(){
      this.$emit("redo");
    },
    discardChanges(){
      this.$emit("discard-changes");
    },
    remove(){
      this.$emit("remove");
    },
    validate(){
      (this.counter === 0) ? this.isUndoBtnDisabled = true : this.isUndoBtnDisabled = false;
      (this.counter === this.length - 1) ? this.isRedoBtnDisabled = true : this.isRedoBtnDisabled = false;
      (this.counter < 1) ? this.isDiscardBtnDisabled = true : this.isDiscardBtnDisabled = false;
    }
  }
};
</script>

<style scoped>
.undoredo__wrap{
  margin-bottom: 1rem;
  padding: 0 1rem;
  display: flex;
  justify-content: center;
}

.undoredo__btn {
    margin: 0 3px;
    padding: 0;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    border: 0;
    outline: none;
    background-color: var(--secondary-blue);
    cursor: pointer;
}

.undoredo__btn:hover{
  background-color: var(--blue);
}

.undoredo__btn:disabled:hover{
  background-color: var(--secondary-blue);
  cursor: default;
}

.undoredo__icon{
  margin: auto;
  color: #fff;
}

.undoredo__icon:before{
  margin-left: 0;
}
</style>