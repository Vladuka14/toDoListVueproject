<template>
    <div>
        <ul>
            <todoitem
                v-for="(todo, i) of todos"
                v-bind:todo="todo"
                v-on:remove-todo="removeTodo"
                v-bind:index="i"
            />
        </ul>
    </div>
</template>
<script>
import todoitem from '@/components/ToDoItem.vue'
export default {
    props:['todos'],
    components:{
        todoitem
    },
    methods:{
        removeTodo(id){
            this.$emit('remove-todo', id)
        }
    }
}
</script>
<style scoped>
    ul{
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>