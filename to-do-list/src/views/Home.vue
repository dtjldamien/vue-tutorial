<template>
  <div id="app">
    <AddToDo v-on:add-todo="addToDo"/>
    <ToDos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import ToDos from '../components/ToDos'
import AddToDo from '../components/AddToDo'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    AddToDo,
    ToDos
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id)  {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));
    },
    
    addToDo(newToDo) {
      const { title, completed } = newToDo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
          }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }  
  
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
