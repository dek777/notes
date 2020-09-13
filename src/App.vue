<template>
  <div id="app">
    <router-link to="/"><h1 class="header__title"><span class="header__title_circle">З</span>аметки</h1></router-link>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/edit">Edit</router-link>
    </div> -->
    <transition name="pages-fade" mode="out-in">
      <router-view :notes="notes" @remove-note="removeNote" />
    </transition>
  </div>
</template>


<script>

export default {
  data(){
    return {
      notes: [
        {
          id: 0,
          title: 'Название заметки №1',
          todos: [
            {
              id: 0,
              completed: false,
              text: 'Задача 1'
            },
            {
              id: 1,
              completed: false,
              text: 'Задача 2'
            }
          ]
        },
        {
          id: 1,
          title: 'Название заметки №2',
          completed: false,
          todos: [
            {
              id: 0,
              text: 'Задача 1'
            },
            {
              id: 1,
              text: 'Задача 2'
            },
            {
              id: 2,
              text: 'Задача 3'
            }
          ]
        }
      ]
    }
  },
  methods: {
    removeNote(id){
      this.notes = this.notes.filter( note => note.id !== id )
    }
  },
  components: {
    
  }
}
</script>

<style>
:root{
  --text: #202224;
  --secondary-text: #7d7d7e;
  --grey: #525252;
  --blue: #4279ee;
  --secondary-blue: #93afec;
  --bg-blue: #E6F2FE;
}

* { 
  box-sizing: border-box;
}

html,body{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  overflow-x: hidden;
  background-color: var(--bg-blue);
}

#app {
  font-family: 'Gilroy', sans-serif;
  font-size: 10px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--text);
}

input{
  font-family: 'Gilroy', sans-serif;
}

a, a:hover, a:focus{
  text-decoration: none;
  color: var(--text);
}

.header__title{
  font-size: 2.5rem;
  width: max-content;
  margin: 1rem auto;
  padding: 15px;
}

.header__title_circle{
  color: #fff;
  background-color: var(--blue);
  padding: 0.2rem 1rem;
  border-radius: 50%;
}

.container{
  width: 100%;
  max-width: 1200px;
  padding: 15px;
  margin: auto;
  box-sizing: border-box;
}

.icon{
  color: var(--secondary-blue);
  margin: 0.3rem 0 1.5rem 0.3rem;
}

.icon:hover{
  color: var(--blue);
  cursor: pointer;
}

/* Animation */

.pages-fade-enter-active,
.pages-fade-leave-active {
  transition: opacity 0.3s;
}

.pages-fade-enter,
.pages-fade-leave-to {
  opacity: 0;
}
</style>
