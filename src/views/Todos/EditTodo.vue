<script>
import TodoService from '@/services/todo.services'
import { onMounted, reactive } from 'vue'
import router from '@/router'
export default {
    name: 'EditTodo',
    props: {
        id: {
            require: true
        }
    },
    setup (props){
        const todo = reactive({
            name:'',
            description: '',
            completed: false,
            loading: false,
        })

        onMounted(()=> {
            todo.loading = true
            TodoService.editTodo(props.id)
                        .then(response => {
                            const todoR = response.data.data
                            todo.name = todoR.title
                            todo.description = todoR.body
                            todo.completed = todoR.completed == 'S'
                        })
                        .finally(() => todo.loading = false)
        })

        const editTodo = () => {
            todo.loading = true
            TodoService.editTodo(props.id, {...todo})
                        .then(()=>router.push({name: 'todos.index'}))
                        .finally(() => todo.loading = false)
        }

        return {    
            editTodo,
            todo,
            
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
                <span v-if="todo.loading">Aguarde...</span>
                <span v-else>Enviar</span>
                
            </button>
        </form>
    </div>
</template>