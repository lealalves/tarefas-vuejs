<template>
    <div id="tasks-show" v-for="task in tasks" :key="task.id">
        <p>{{task.descricao}}</p>
        <font-awesome-icon id="remove-btn" icon="trash-alt"  style="color: #222;" @click="removeTask(task.id)"/>
    </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core'
import { faTrashAlt } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(faTrashAlt)

export default {
    name: 'TaskShow',
    components: {
        FontAwesomeIcon
    },
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
        },
        async removeTask(id) {

            const req = await fetch(`http://localhost:3000/tarefas/${id}`, {
                method: "DELETE"
            })
            
        }
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
        margin-top: 10px;
        padding: 10px;
        border: 1px solid rgb(255, 255, 255);
        background-color: rgb(255, 255, 255);
        border-radius: 10px;
    }
    #tasks-show p{
        max-width: 500px;
        color: black;
        font-weight: bold;
        word-wrap: break-word;
    }
    #remove-btn{
        margin-left: 10px;
        cursor: pointer;
    }
</style>