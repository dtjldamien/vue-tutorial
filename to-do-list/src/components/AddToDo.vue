<template>
    <div>
        <form @submit="addToDo">
            <input type="text" v-model="title" placeholder="Add To Do...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// import { v4 as uuidv4 } from 'uuid'

export default {
    name: "AddToDo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addToDo(e) {
            e.preventDefault();
            const newToDo = {
                // id: uuidv4(),
                title: this.title,
                completed: false
            }
                    
            // Send up to parent
            this.$emit('add-todo', newToDo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }
</style>
