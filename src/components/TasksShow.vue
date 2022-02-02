<template>
    <div id="tasks-show" :class="{feita: task.status}" v-for="task in tasks" :key="task.id">
        <div id="task-infos">
            <p id="task-name" @click="updateTask(task.status, task.id)">{{task.nome}}</p>
            <p id="task-desc">{{task.descricao}}</p>
        </div>
        <router-link :to=" {
            name: 'Detalhes', 
            params: {
                task_id: task.id,
                task_name: task.nome,
                task_desc: task.descricao
                }
            }">
        <font-awesome-icon icon="edit" style="color: #222;" id="fontawesome-icon"/>
        </router-link>
        <font-awesome-icon icon="trash-alt" style="color: #222;" id="fontawesome-icon" @click="removeTask(task.id)"/>
    </div>
    <h1 id="no-task-msg" v-show="tasks == ''">nenhuma tarefa encontrada.</h1>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faTrashAlt } from '@fortawesome/free-solid-svg-icons'
import { faEdit } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faTrashAlt, faEdit)

export default {
    name: 'TaskShow',
    components: {
        FontAwesomeIcon
    },
    data(){
        return {
            tasks: null,
        }
    },
    methods: {
        async getTasks() {
            const req = await fetch('http://localhost:3000/tarefas')

            const data = await req.json()

            this.tasks = data
        },
        async removeTask(id) {

            const req = await fetch(`http://localhost:3000/tarefas/${id}`, {
                method: "DELETE"
            })
            
        },
        async updateTask(status, id) {

            const dataJson = JSON.stringify({ status: !status })

            const req = await fetch(`http://localhost:3000/tarefas/${id}`, {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            })

        },
    },
    mounted() {
        setInterval(() => {
            this.getTasks()
        }, 500);
    }
}
</script>

<style scoped>
    #tasks-show{
        display: flex;
        align-items: center;
        margin-top: 10px;        
        border: 1px solid whitesmoke;
        background-color: whitesmoke;
        border-radius: 10px;
        transition: .5s;
        padding: 5px;
    }
    #tasks-show.feita{
        border-left: 10px solid rgb(47, 255, 116);
    }
    #task-name{
        max-width: 500px;
        color: black;
        font-weight: bold;
        font-size: 18px;
        word-wrap: break-word;
        padding: 5px;
        cursor: pointer;
    }
    #task-desc{
        color: #222;
        font-size: 12px;
        font-style: italic;
        padding-left: 8px;
        max-width: 300px;
    }
    #fontawesome-icon{
        margin-left: 10px;
        cursor: pointer;
    }
    #no-task-msg{
        margin-top: 50px;
        font-size: 16px;
    }
</style>