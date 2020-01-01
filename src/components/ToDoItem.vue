<template>
    <div class="container">
        <div class="row">
            <div class="col-lg-1">
               <input id="checkbox" type="checkbox" v-on:change="todo.completed = !todo.completed">
            </div>
            <div class="col-lg-9">
               <div id="maintext" v-bind:class="{done: todo.completed}"><strong>{{(index+1)}}</strong> {{todo.title | uppercase}}</div>
            </div>
            <div class="col-lg-2">
                <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        props:{
            todo:{
                type:Object,
                required:true
            },
            index:Number
        },
        filters:{
            uppercase(value){
                return value.toUpperCase()
            }
        }
    }
</script>
<style scoped>
    span{
        display: flex;
    }
    li{

    }
    .rm{
        margin-left: 70%;
        background: azure;
        border-radius: 30px;
        border: 3px solid #17a2b8;
        font-weight: bold;
        font-size: 20px;
        color: #17a2b8;
        height: 40px;
        width: 40px;
    }
    .rm:hover{
        background: #17a2b8;
        color: white;
    }
    .done{
        text-decoration: line-through;
    }
    input{

    }
    .line{

    }
    #maintext{
        text-align: left;
        font-size: 30px;
    }
    #maintext strong{
        padding-right: 15px;
    }
    #checkbox{
        height: 30px;
        width: 30px;
        margin-top: 8px;
    }
</style>