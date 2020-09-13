<template>
  <div class>
    <button class="btn__new-note" @click.prevent="showHideForm">Новая заметка</button>
    <FormCreateNote :formVisible="formVisible" @init-note="createNote" @hide-form="showHideForm" />
  </div>
</template>

<script>
import FormCreateNote from "@/components/FormCreateNote.vue";

export default {
  data() {
    return {
      formVisible: false
    };
  },
  methods: {
    showHideForm() {
      this.formVisible = !this.formVisible;
    },
    createNote(note){
      this.$emit("create-note", JSON.parse(note));
      this.formVisible = false;
    }
  },
  components: {
    FormCreateNote,
  },
};
</script>

<style scoped>
.btn__new-note {
  margin: 2rem auto;
  padding: 15px 25px;
  background-color: var(--blue);
  color: #fff;
  text-transform: uppercase;
  font-weight: 600;
  border: 0;
  cursor: pointer;
  border-radius: 5px;
}
.btn__new-note:hover,
.btn__new-note:focus {
  border: 0;
  outline: none;
}
.btn__new-note:hover {
  background-color: #326ff3;
  color: #fff;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  -moz-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
}

</style>