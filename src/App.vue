<template>
  <div id="app">
   <header>
     <h1>TodoList</h1>
   </header>
   <main>
     <section id="container-todolist">

     </section>
   </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  }
}
</script>

<style lang="scss">

@import './assets/scss/index.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;

  header {
    padding: 10px;
    h1 {
      font-size: 60px;
      font-weight: bold;
      text-align: center;
    }
  }
}
</style>
