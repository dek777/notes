<template>
  <div class="note__card">
    <div class="note__title-wrap">
      <p class="note__title">{{note.title}}</p>
      <div class="icons__wrap">
        <router-link :to="{ path: '/edit', query: {id: note.id} }" :note="note"><i class="flaticon-pencil icon"></i></router-link>
        <i class="flaticon-delete icon" @click="showHideConfirmModal"></i>
      </div>
    </div>
  
    <ConfirmModal :confirmModalVisible="confirmModalVisible" @delete-item="deleteNote" @cancel="showHideConfirmModal" />

    <TodoList :todos="note.todos" />
    <TodoTotals :todosCount="note.todos.length" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoTotals from "@/components/TodoTotals.vue";
import ConfirmModal from "@/components/ConfirmModal.vue";

export default {
  data(){
    return{
      confirmModalVisible: false,
    }
  },
  props: {
    note: {
      type: [Object, Array],
      required: true,
    },
  },
  methods: {
    showHideConfirmModal(){
      this.confirmModalVisible = !this.confirmModalVisible;
    },
    deleteNote(){
      this.$emit('delete-note', this.note.id);
    },
  },
  components: {
    TodoList,
    TodoTotals,
    ConfirmModal
  },
};
</script>

<style scoped>
.note__card {
  padding: 15px 20px;
  border-radius: 10px;
  background-color: #fff;
  text-align: left;
  -webkit-box-shadow: 0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  -moz-box-shadow:    0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  box-shadow:         0px 5px 10px 0px rgba(50, 50, 50, 0.3);
  position: relative;
  min-height: 219px;
  box-sizing: border-box;
}

.note__title {
  font-size: 1.1rem;
  font-weight: 600;
  margin: 0.3rem 0 1.5rem;
}

.note__title-wrap {
  display: flex;
  justify-content: space-between;
}

.icons__wrap{
  padding: 5px;
}


</style>