<template>
  <div v-if="confirmBlockVisible" class="">
    <p class="confirm__text">Удалить?</p>
    <button class="confirm__btn confirm__btn_yes" @click.prevent="">Да</button>
    <button class="confirm__btn confirm__btn_no" @click.prevent="">Нет</button>
  </div>
</template>

<script>
export default {
  props: {
    confirmBlockVisible: {
      type: Boolean
    }
  },
  methods: {
    deleteItem(){
      this.$emit('delete-item');
    },
    cancel(){
      this.$emit('cancel');
    }
  }
}
</script>

<style scoped>

</style>