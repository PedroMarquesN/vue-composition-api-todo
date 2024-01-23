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
    </div>
</template>

