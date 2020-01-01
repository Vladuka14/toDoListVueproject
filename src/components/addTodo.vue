<template>
    <form @submit.prevent="onSubmit">
        <input type="text" v-model="title" placeholder="Введите ваше деловое дело">
        <button class="createBtn" type="submit">Создать</button>
    </form>
</template>
<script>
    export default {
        data() {
            return{
                title: ''
            }
        },
        methods:{
            onSubmit(){
                if (this.title.trim()){
                   const newTodo = {id: Date.now(),
                    title:this.title,
                    completed:false
                   }
                   this.$emit('add-todo', newTodo)
                   this.title='';
                }
            }
        }
    }
</script>
<style>
    input{
        width: 100%;
        padding-left: 10px;
        border: 0;
        border-radius: 5px;

    }
    form{
        display: flex;
        width: 100%;
        height: 50px;
        border-radius: 5px;
        border: 0.5px solid #7a7a7a;
    }
    .createBtn{
        background: #17a2b8;
        color: azure;
        border: 0;
        border-radius: 0 5px 5px 0;
        font-weight: bold;
        font-size: 15px;

    }
</style>