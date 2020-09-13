<template>
  <div class="edit__wrap">
    <h2>Edit</h2>
   <p>{{editNote}}</p>
  </div>
</template>


<script>
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
  }
}
</script>

<style scoped>

</style>