<template>
  <div class="container">
    <CreateNote v-on:create-note="createNewNote" />
    <div v-if="notes.length" class="notes__wrap">
      <Note v-for="note in notes" :key="note.id" :note="note" @delete-note="deleteNote" />
    </div>
    <p v-else class="text_empty-list">Нет заметок</p>
    
  </div>
</template>

<script>
import Note from '@/components/Note.vue'
import CreateNote from '@/components/CreateNote.vue'

export default {
  name: 'Home',
  props: {
    notes: {
      type: [Object, Array]
    }
  },
  methods: {
    createNewNote(note){
      this.notes.unshift(note);
    },
    deleteNote(id){
      this.$emit('remove-note',id);
    }
  },
  components: {
    Note, CreateNote
  }
}
</script>


<style scoped>
.notes__wrap{
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 2rem;
  margin: 2rem auto;
}

.text_empty-list{
  font-size: 1.1rem;
  color: var(--secondary-text);
}
</style>