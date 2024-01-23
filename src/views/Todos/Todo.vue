<script>
import TodoService from '@/services/todo.services'
import { computed } from 'vue'
export default {
    name: 'Todo',
    props: {
        todo:{
            require:true,
            type: Object,
        }

    },
    setup(props, {emit}){
        const completed = computed(() => props.todo.completed == 'S')
 
        const deleteTodo = () => {
                TodoService.deleteTodo(props.todo.indentify)
                            .then(() => emit('todoDeleted', props.todo))
            }
        const toogleStatus = () =>{
            const todo = props.todo
            const params = {
                name: todo.title,
                description: todo.body,
                completed: !completed.value
            }
            TodoService.editTodo(props.todo.indentify, params)
                        .then(() => emit('todoUpdated' , params))
        }

            return {
                deleteTodo,
                completed,
                toogleStatus
            }
    }

    
}
</script>

<template >
    <div>
        {{todo.title}}   -   {{ todo.body }}
        <input type="checkbox" :checked="completed" @change="toogleStatus">
        <router-link :to="{name:'todos.edit', params: {id:todo.indentify}}">Edit</router-link>
        <a href="#" @click.prevent="deleteTodo">Deletar</a>
    </div>
</template>

