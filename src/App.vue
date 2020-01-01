<template>
  <div id="app">
    <myHeader/>
    <router-view/>
    <myFooter/>
  </div>
</template>

<script>
import myHeader from '@/components/header'
import toDoList from '@/components/ToDoList'
import addTodo from '@/components/addTodo'
import myFooter from '@/components/footer'
export default {
  name: 'app',
  data(){
    return{
      todos:[]
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
            .then(response => response.json())
            .then(json => {
              this.todos = json
            })
  },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !== id )
    },
    addTodo(todo){
      this.todos.push(todo)


    }
  },
  components: {
    toDoList,
    addTodo,
    myHeader,
    myFooter
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
