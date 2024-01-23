<script>
export default {
    name: 'Todo',
    props: {
        todo:{
            require:true,
            type: Object,
        }

    }
}
</script>

<template >
    <div>
        {{todo.title}}   -   {{ todo.body }}

        <router-link :to="{name:'todos.edit', params: {id:todo.indentify}}">Edit</router-link>
    </div>
</template>

