<template>
    <ul class="list-group list-group-flush border">
        <li v-for="(todo, index) in tasksListView" :key="index" class="list-group-item" :class="{'list-group-item-line-through list-group-item-danger': todo.checked}" >
            <div class="input-group">
                <div class="input-group-prepend">
                    <div class="input-group-text">
                        <input type="checkbox" v-model="todo.checked" @click="todo.toggleChecked(),updateTasksStats()">
                    </div>
                </div>
                <input class="form-control w-50 float-center" v-bind:value="todo.todo" v-on:change="updateTaskName($event,todo)">
                <div class="input-group-append">
                    <button type="button" class="btn btn-outline-secondary" aria-label="Close" @click.stop="deleteTask(todo)">x</button>
                </div>
            </div>
        </li>
    </ul>
</template>

<script>
    export default {
        name: "TaskItem",
        props :{
            tasksListView : { type: Array},
            updateTasksStats:{type: Function},
            deleteTask:{type: Function},
            updateTaskName:{type: Function}
        }
    }
</script>

