<script>
import TodoService from '@/services/todo.services'
import { reactive } from 'vue'
import router from '@/router'
export default {
    name: 'AddTodo',
    setup (){
        const todo = reactive({
            name:'',
            'description': '',
            completed: false,
            loading: false,
        })
        const addTodo = () => {
            todo.loading = true
            TodoService.addTodo({...todo})
                        .then(()=>router.push({name: 'todos.index'}))
                        .finally(() => todo.loading = false)
        }

        return {    
            addTodo,
            todo
        }
    }
}
</script>

<template>
    <div>
        <h1>Adicionar nova Tarefa</h1>

        <form action="#" method="post" @submit.prevent="addTodo">
            <input type="text" name="title" placeholder="Nome" v-model="todo.name">
            <input type="text" name="description" placeholder="Descrição" v-model="todo.description">
            <button type="submit" :disable="todo.loading">
                <span v-if="todo.loading">Enviando...</span>
                <span v-else>Enviar</span>
                
            </button>
        </form>
    </div>
</template>