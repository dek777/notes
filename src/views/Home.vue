<template>
  <div class="container">
    <h2></h2>

    <div class="notes__wrap">
      <Note v-for="note in notes" :key="note.id" :note="note" />
    </div>
    
  </div>
</template>

<script>
import Note from '@/components/Note.vue'

export default {
  name: 'Home',
  props: {
    notes: {
      type: [Object, Array],
      required: true
    }
  },
  components: {
    Note
  }
}
</script>


<style scoped>
.notes__wrap{
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 2rem;
}
</style>