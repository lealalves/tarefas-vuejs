<template>
    <div id="tasks-show" :class="{feita: task.status}" v-for="task in tasks" :key="task.id">
        <p @click="updateTask(task.status, task.id)">{{task.nome}}</p>
        <font-awesome-icon icon="trash-alt" style="color: #222;" id="fontawesome-icon" @click="removeTask(task.id)"/>
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
    </div>
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
        cursor: pointer;
        transition: .5s;
        padding: 5px;
    }
    #tasks-show.feita{
        border-left: 10px solid rgb(47, 255, 116);
    }
    #tasks-show p{
        max-width: 500px;
        color: black;
        font-weight: bold;
        word-wrap: break-word;
        padding: 5px;        
    }
    #fontawesome-icon{
        margin-left: 5px;
        cursor: pointer;
    }
</style>