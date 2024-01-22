<script>
import TodoService from '@/services/todo.services'
import { onMounted, ref } from 'vue'


export default {
 name: 'TodosIndex',
 setup(){

     const todos = ref([])

    onMounted(() => {

        TodoService.getAll()
                .then(response =>{
                    console.log(response)
                    todos.value = response.data.data
                })
                .catch(error => console.log(error))
    })
    return {
        todos,
    }

 }
}
</script>

<template>
    <h1>Lista de tarefas</h1>

    <ul>
        <li v-for="todo in todos" :key="todo.indentify">
            {{ todo.title }}
        </li>
    </ul>
</template>