<template>    
    <form id="form-input" @submit="addTask($event)">
        <h1>tarefa:</h1>
        <input type="text" name="task" id="task-input" v-model="task">
        <input type="submit" id="task-btn" value="Adicionar">
    </form>
</template>

<script>
export default {
    name: 'TaskInput',
    data(){
        return {
            task: null
        }
    },
    methods: {
        async addTask(e) {
            e.preventDefault()

            const data = {
                descricao: this.task,
                status: false
            }

            const dataJson = JSON.stringify(data)
            
            const req = await fetch('http://localhost:3000/tarefas', {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })

            const res = await req.json()

        }
    }
}
</script>

<style scoped>
    #form-input {
        display: flex;
        width: 100%;
        height: 50px;
        align-items: center;
        justify-content: space-evenly;
    }
    #task-input{
        height: 30px;
        padding: 10px;
        border: none;
        caret-color: indianred;
        color: whitesmoke;
        background-color: white;
        border-radius: 10px;
    }
    #task-btn{
        width: auto;
        padding: 10px;
        border: 1px solid white;
        background-color: white;
        color: black;
        font-weight: bold;
        border-radius: 10px;
        transition: .5s;
    }
    #task-btn:hover{
        background-color: transparent;
        color: white;
    }
</style>