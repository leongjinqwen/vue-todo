<template>
  <div>
    <div class="panel-block" >
      <div v-bind:class="{'completed':todo.completed}">{{todo.title}}</div>
      <div>
        <button class="button is-small is-rounded is-primary" v-on:click="markDone" >
          <span v-if="todo.completed">Undone</span>
          <span v-else>Done</span>
        </button>
        <button class="button is-small is-rounded is-danger" @click="$emit('del-todo', todo.id)" >Del</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ToDoItem',
  props: ["todo"],
  methods: {
    markDone() {
      axios.put(`https://jsonplaceholder.typicode.com/todos/${this.todo.id}`)
      .then( res => {
          this.todo.completed = !this.todo.completed;
          console.log(res.data) 
        }
      )
      .catch( err => console.log(err))
      // this.todo.completed = !this.todo.completed;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .panel-block {
    justify-content: space-between;
  }
  .done {
    text-decoration: line-through;
    color: red;
  }
</style>
