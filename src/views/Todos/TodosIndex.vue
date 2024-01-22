<script>
import TodoService from '@/services/todo.services'
import { onMounted, ref } from 'vue'


export default {
 name: 'TodosIndex',
 setup(){

     const todos = ref([])
     const loading = ref(false)

    onMounted( async () => {
        loading.value = true
        TodoService.getAll()
                .then(response =>{
                    console.log(response)
                    todos.value = response.data.data
                })
                .catch(error => console.log(error))
                .finally(()=> loading.value = false)
    })
    return {
        todos,
        loading,
    }

 }
}
</script>

<template>
    <h1>Lista de tarefas</h1>
    <router-link :to="{name:'todos.create'}">+</router-link>
    <div v-if="loading">Carregando...</div>
    <ul>
        <li v-for="todo in todos" :key="todo.indentify">
            {{ todo.title }}
        </li>
    </ul>
</template>