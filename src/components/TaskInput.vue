<template>    
    <form id="form-input" @submit="addTask($event)">
        <input type="text" name="task" id="task-input" :class="{error: this.error}" v-model="task" placeholder="O que está pensando?">
        <Button msg="Adicionar"/>
    </form>
</template>

<script>
import Button from './Button.vue'


export default {
    name: 'TaskInput',
    components: {
        Button
    },
    data(){
        return {
            task: null,
            error: false
        }
    },
    methods: {
        async addTask(e) {
            e.preventDefault()

            if(this.task != null){

                const data = {
                    nome: this.task,
                    status: false,
                    descricao: "Insira uma descrição sobre a tarefa!"
                }
    
                const dataJson = JSON.stringify(data)
                
                const req = await fetch('http://localhost:3000/tarefas', {
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: dataJson
                })
    
                const res = await req.json()
    
                this.task = null

            }else {
                this.error = true
                setInterval(() => {
                    this.error = false
                }, 3000);
            }


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
        border: 2px solid white;
        background-color: white;
        box-shadow: 0 0 0 transparent;
        border-radius: 10px;
        margin-left: 10px;
        width: 300px;
        transition: .2s;
    }
    #task-input.error{
        box-shadow: 0 0 0.5em red;
        animation: shake 0.2s ease-in-out 0s 2;
    }

    @keyframes shake {
    0% { margin-left: 0rem; }
    25% { margin-left: 0.5rem; }
    75% { margin-left: -0.5rem; }
    100% { margin-left: 0rem; }
    }
</style>