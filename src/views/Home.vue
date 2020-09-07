<template>
  <div class="container">
    <CreateNote />
    <div class="notes__wrap">
      <Note v-for="note in notes" :key="note.id" :note="note" />
    </div>
    
  </div>
</template>

<script>
import Note from '@/components/Note.vue'
import CreateNote from '@/components/CreateNote.vue'

export default {
  name: 'Home',
  props: {
    notes: {
      type: [Object, Array],
      required: true
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
</style>