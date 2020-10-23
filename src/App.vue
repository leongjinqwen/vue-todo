<template>
  <div id="app">
    <section class="hero is-dark is-bold">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            To Do List
          </h1>
        </div>
      </div>
    </section>
    <article class="panel is-warning">
      <ToDoForm v-on:add-todo="addTodo" />
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTask" />
    </article>
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import ToDoForm from './components/ToDoForm.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    ToDoForm,
    Todos
  },
  data(){
    return {
      todos: []
    }
  },
  methods: {
    deleteTask(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then( res => {
          this.todos = this.todos.filter(todo=>todo.id !== id)
          console.log(res.data) 
        }
      )
      .catch( err => console.log(err))
    },
    addTodo(obj) {
      const {title, completed} = obj
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, 
        completed
      })
      .then( res => this.todos = [...this.todos, res.data])
      .catch( err => console.log(err))
    },
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then( res => this.todos = res.data)
    .catch( err => console.log(err))
  }
}
</script>

<style>
  body {
    font-family: 'Montserrat', sans-serif;
  }
  section.hero {
    background-image: url('https://i1.wp.com/codemyui.com/wp-content/uploads/2016/11/pure-css-snow-animation.gif?fit=880%2C440&ssl=1') !important;
  }
  article {
    margin: -25px 25px 25px 25px;
  }
  
</style>
