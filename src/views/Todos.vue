<template>
    <div>
        <h2>Режим работы со списком задач</h2>
        <router-link to="/">Вернуться на главную</router-link>
        <hr>
        <div class="container">
            <div class="row">
                <div class="col-lg-9">
        <addTodo
                @add-todo="addTodo"
        />
                </div>
                <div class="col-lg-3">
        <select class="typeOfTodo" v-model="filter">
            <option value="all">Все задачи</option>
            <option value="completed">Выполненные</option>
            <option value="not-completed">Не выполненные</option>
        </select>
                </div>
            </div>
        </div>
        <hr>
        <loader
                v-if="loading"
        />


        <toDoList
                v-else-if="filteredTodos.length"
                v-bind:todos="filteredTodos"
                @remove-todo="removeTodo"
        />
        <p v-else>Шок контент! Дела закончились ( Пора придумывать новые... </p>

    </div>
</template>
<script>
    import toDoList from '@/components/ToDoList'
    import addTodo from '@/components/addTodo'
    import loader from '@/components/loader'
    export default {
        name: 'app',
        data(){
            return{
                todos:[],
                loading:true,
                filter: 'all'
            }
        },
        mounted(){
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
                .then(response => response.json())
                .then(json => {
                    setTimeout(()=>{
                        this.todos = json
                        this.loading = false
                    }, 1000)

                })
        },
        /*watch:{
          filter(value){
              console.log(value);
          }
        },*/
        computed: {
          filteredTodos(){
              if (this.filter === 'all'){
                  return this.todos
              }
              if (this.filter === 'completed'){
                  return this.todos.filter(t=> t.completed)
              }
              if (this.filter === 'not-completed'){
                  return this.todos.filter(t=> !t.completed)
              }
          }
        },
        methods: {
            removeTodo(id){
                this.todos = this.todos.filter(t => t.id !== id )
            },
            addTodo(todo){
                console.log(todo)
                this.todos.push(todo)


            }
        },
        components: {
            toDoList,
            addTodo,
            loader
        }
    }
</script>
<style>
    .typeOfTodo{
        height: 50px;
        width: 100%;
        padding-left: 10px;
    }
</style>