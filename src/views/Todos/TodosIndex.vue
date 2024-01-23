<script>
import TodoService from '@/services/todo.services'
import { onMounted, ref } from 'vue'
import Todo from './Todo.vue'


export default {
 name: 'TodosIndex',
 setup(){

     const todos = ref([])
     const loading = ref(false)

    onMounted( async () => {
        loading.value = true
        TodoService.getAll()
                .then(response =>{
                    todos.value = response.data.data
                })
                .catch(error => console.log(error))
                .finally(()=> loading.value = false)
    })

    const removeTodoList = (todo) => todos.value.splice(todos.value.indexOf(todo), 1)

    const todoUpdated = (todo) => {
        todos.value[todos.value.indexOf(todo)] = todo
    }
    return {
        todos,
        loading,
        removeTodoList,
        todoUpdated
    }
    
},
components: {
    Todo 
}
}
</script>

<template>
    <h1>Lista de tarefas</h1>
    <router-link :to="{name:'todos.create'}">+</router-link>
    <div v-if="loading">Carregando...</div>
    <ul>
        <li v-for="todo in todos" :key="todo.indentify">
           <todo :todo="todo" @todoDeleted="removeTodoList" @todoUpdated="todoUpdated" />
        </li>
    </ul>
</template>