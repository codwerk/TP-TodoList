<template>
  <div id="app">
      <header class="header">
       <h1>TP : TodoList</h1>
      </header>
     <section class="todoapp">
       <header class="todoapp__hdr">
         <input type="text" class="new-todo" placeholder="Ajoute une tâche" v-model="newTodo" @keyup.enter="addTodo">
       </header>
       <div class="todoapp__body">

         <div class="wrapper__option">
          <input type="checkbox" v-model="allDone">
          <label> Tous sélectionner </label>
         </div>

         <ul class="todo-list">
           <li class="todo" v-for="(todo, index) in filtered" :key="index">
             <div class="view">
               <input type="checkbox" v-model="todo.completed">
               <label  :class="{completed: todo.completed}">{{ todo.name }}</label>
               <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
             </div>
           </li>
         </ul>
       </div>
       <footer class="todoapp__ftr" v-if="todos.length > 0">
         <div class="wrapper-ftr__option">
          <span class="todo-count"> {{ remaining }} {{ remaining > 1 ? 'tâches' : 'tâche'}}  a réalisée</span>
          <button v-show="completed" @click.prevent="deleteCompleted">Supprimer tâche réalisée</button>
         </div>
         
         <ul class="todoapp__ftr-list">
           <li><a href="#" :class="{selected: filter === 'all'}"  @click.prevent="filter = 'all'">Toutes</a></li>
           <li><a href="#" :class="{selected: filter === 'todo'}"  @click.prevent="filter = 'todo'">A faire</a></li>
           <li><a href="#" :class="{selected: filter === 'done'}"  @click.prevent="filter = 'done'">Faites</a></li>
         </ul>
         
       </footer>
     </section>
  </div>
</template>

<script>


export default {
  name: 'App',
  data () {
    return {
      todos: [],
      newTodo: '',
      filter: ''
    }
  }, 
  methods: {
    addTodo() {
      this.todos.push({
        name: this.newTodo,
        completed: false
      })
      
      this.newTodo = ''
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter(i => i !== todo)
    },
    deleteCompleted () {
     this.todos = this.todos.filter( todo => !todo.completed)
    }
  },
  computed: {
    allDone: {
      get (){
        return false;
      },
      set (value) {
        console.log('value', value);
          this.todos.forEach( todo => {
            todo.completed = value
          })
      }
    },
    remaining () {
     return this.todos.filter( todo => !todo.completed).length
    },
    completed () {
     return this.todos.filter( todo => todo.completed).length
    },
    filtered () {
      if(this.filter === 'todo'){
        return this.todos.filter( todo => !todo.completed)
      } else if(this.filter === 'done') {
        return this.todos.filter( todo => todo.completed)
      }
      return this.todos
    }
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

  .header {
    padding: 10px;
    h1 {
      font-size: 60px;
      font-weight: bold;
      text-align: center;
    }
  
  }
  .todoapp {
    max-width: 80%;
    margin: 0 auto;
    padding: 0 10px;

    .todoapp__hdr {
      text-align: center;

      .new-todo {
        border: none;
        border-bottom: 1px solid #2c3e50;
        padding: 10px;
        outline: none;
      }
    }

    .todoapp__body {
      margin: 0 20px;

      .wrapper__option {
        text-align: center;
        margin: 20px 0px;
      }
      .todo-list {
        margin: 20px 0;

        .todo {
          max-width: 50%;
          margin: 0 auto;
          .view {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;

            input[type="checkbox"] {
              cursor: pointer;
              
            }

            label {
              text-transform: capitalize;
            }

            .destroy {
              position: relative;
              border: none;
              cursor: pointer;
              background: transparent;
              &::after {
                content: '-';
                position: absolute;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                font-size: 30px;
                font-weight: 100;
              }
            }
          }
        }
      }
    }

    .todoapp__ftr {
      margin: 20px 0;
      max-width: 50%;
      margin: 0 auto;

      .wrapper-ftr__option {
        display: flex;
        justify-content: space-between;
      }

      .todoapp__ftr-list {
        
        display: flex;
        justify-content: space-between;
        padding: 10px 0px;

        li {
          padding: 5px;

          a {
            padding: 5px;
            text-decoration: none;
            color :#2c3e50;
            border: 1px solid #fff;
            border-radius: 5px;

          }

          a.selected {
                border: 1px solid #000;
              }
        }
      }
    }

  }

  .completed {
    color: rgb(185, 178, 178);
    position: relative;

    &::before {
      content: '';
      position: absolute;
      width: 100%;
      height: 1px;
      background: #2c3e50;
      top: 10px;
      right: 0;
    }
  }


}
</style>
