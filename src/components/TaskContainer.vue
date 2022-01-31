<template>
    <div id="task-container">
        <TaskInput />
        <TasksShow />
    </div>
</template>

<script>
import TaskInput from "../components/TaskInput.vue"
import TasksShow from "../components/TasksShow.vue"

export default {
    name: 'TaskContainer',
    components: {
        TaskInput,
        TasksShow
    }
}
</script>

<style scoped>
    #task-container{
        display: flex;
        align-items: center;
        flex-direction: column;
        border: 1px solid #222;
        min-width: 700px;
        min-height: 500px;
        background-color: #222;
        border-radius: 10px;
        color: honeydew;
        padding: 10px;
    }
</style>