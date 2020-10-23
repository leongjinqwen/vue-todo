<template>
  <div>
    <div class="container" v-bind:key="todo.id" v-for="todo in todos">
      <ToDoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import ToDoItem from "./ToDoItem"

export default {
  name: 'Todos',
  components: {
    ToDoItem
  },
  props: ["todos"]
}
</script>

