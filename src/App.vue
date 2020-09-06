<template>
  <div id="app">
    <h1 class="header__title"><span class="header__title_circle">З</span>аметки</h1>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/edit">Edit</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
html,body{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  overflow-x: hidden;
  background-color: #E6F2FE;
}

#app {
  font-family: 'Gilroy', sans-serif;
  font-size: 10px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #202224;
}

.header__title{
  font-size: 2.5rem;
  width: max-content;
  margin: 1rem auto;
  padding: 15px;
}

.header__title_circle{
  color: #fff;
  background-color: #4279EE;
  padding: 0.2rem 1rem;
  border-radius: 50%;
}

.container{
  width: 100%;
  max-width: 1200px;
  padding: 15px;
}

/* #nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #202224;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
