<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <ToDoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
        </div>
    </div>
</template>

<script>
import ToDoItem from './ToDoItem'

export default {
    name: "ToDos",
    components: {
        ToDoItem
    },
    props: ["todos"]
}
</script>

<style scoped>

</style>