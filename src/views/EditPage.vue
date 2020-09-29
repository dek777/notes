<template>
  <div class="edit__wrap">
    <h1 class="title">Редактирование заметки</h1>
    <FormEditNote :note="editNote" @delete-note="deleteNote" @save-note="saveNote" />
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
    },
    deleteNote(id) {
      this.$emit("remove-note", id);
      this.$router.push('/');
    },
    saveNote(oldNote, newNote){
      oldNote.title = newNote.title;
      oldNote.todos = newNote.todos;
      localStorage.setItem('notes', JSON.stringify(this.notes));
      this.$router.push('/');
    }
  },
  components: {
    FormEditNote
  }
}
</script>

<style scoped>
.title{
  margin: 2rem auto 1rem;
  font-size: 1.4rem;
}
</style>