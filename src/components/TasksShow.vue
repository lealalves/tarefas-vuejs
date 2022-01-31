<template>
    <div id="tasks-show" v-for="task in tasks" :key="task.id">
        <p>{{task.descricao}}</p>
    </div>
</template>

<script>
export default {
    name: 'TaskShow',
    data(){
        return {
            tasks: null
        }
    },
    methods: {
        async getTasks() {
            const req = await fetch('http://localhost:3000/tarefas')

            const data = await req.json()

            this.tasks = data
        }
    },
    mounted() {
        // setInterval(() => {
        //     this.getTasks()
        // }, 500);
    }
}
</script>

<style scoped>
    #tasks-show{
        margin-top: 10px;
        padding: 10px;
        border: 1px solid rgb(255, 255, 255);
        background-color: #333;
        border-radius: 10px;
    }
    #tasks-show p{
        max-width: 500px;
        word-wrap: break-word;
    }
</style>