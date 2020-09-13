<template>
  <div class="edit__wrap">
    <h1>Редактирование заметки</h1>
    <FormEditNote :note="editNote" />
  </div>
</template>


<script>
import FormEditNote from "@/components/FormEditNote.vue"

export default {
  data(){
    return {
      editNote: this.getNote()
    } 
  },
  props: {
    notes: {
      type: [Object, Array]
    }
  },
  methods: {
    getId(){
      return this.$route.query.id
    },
    getNote(){
      const id = this.getId()
      return this.notes.filter( note => note.id == id )[0]
    }
  },
  components: {
    FormEditNote
  }
}
</script>

<style scoped>

</style>