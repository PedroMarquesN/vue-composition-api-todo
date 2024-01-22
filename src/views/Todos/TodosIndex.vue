<script>
import TodoService from '@/services/todo.services'
import { onMounted } from 'vue'


export default {
 name: 'TodosIndex',
 setup(){


    onMounted(() => {
        TodoService.getAll()
                .then(response =>{
                    console.log(response)
                })
                .catch(error => console.log(error))
    })

 }
}
</script>

<template>
    <h1>Lista de tarefas</h1>
</template>