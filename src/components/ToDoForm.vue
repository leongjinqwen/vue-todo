<template>
  <div>
    <p class="panel-heading">
      Add new task:
    </p>
    <div class="panel-block">
      <p class="control">
        <input v-model="title" name="title" class="input is-warning" @keyup.enter="addTodo" type="text" placeholder="Add todo...">
      </p>
    </div>
  </div>
</template>

<script>
  import { v4 as uuidv4 } from 'uuid';

  export default {
    name: 'ToDoForm',
    data(){
      return {
      title: ''
      }
    },
    methods: {
      addTodo() {
        const newTodo = {
          id: uuidv4(),
          title: this.title,
          completed: false
        }
        this.title = ''
        this.$emit('add-todo', newTodo)
      }
    }
  }
</script>

