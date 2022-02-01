<template>    
    <form id="form-input" @submit="addTask($event)">
        <input type="text" name="task" id="task-input" v-model="task" placeholder="O que está pensando?">
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

            if(this.task != null){

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
    
                this.task = null

            }else alert('escreva alguma coisa bobao')


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
        justify-content: center;
    }
    #task-input{
        height: 30px;
        padding: 10px;
        border: none;
        color: rgb(0, 0, 0);
        background-color: white;
        border-radius: 10px;
        margin-left: 10px;
        width: 300px;
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
        margin-left: 10px;
        cursor: pointer;
    }
    #task-btn:hover{
        background-color: transparent;
        color: white;
    }
</style>