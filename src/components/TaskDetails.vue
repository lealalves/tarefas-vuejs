<template>
    <div id="container-principal">
        <div id="task-container">
            <div id="task-details-header">
                <router-link to="/"><Button msg="Voltar"/></router-link>
                <h1>{{task_name}}</h1>
            </div>
            <h3>Descrição</h3>
            <textarea v-model="task_desc_data" :placeholder="task_desc" id="task-details-text" cols="30" rows="10"></textarea>
            <Button msg="Salvar" @click="setTaskDesc"/>
        </div>      
    </div>
</template>

<script>
import Button from './Button.vue'

export default {
    name: 'TaskDetails',
    components: {
        Button
    },
    props: {
        task_id: String,
        task_name: String,
        task_desc: String
    },
    data() {
        return {
            task_desc_data: 'Insira uma descrição sobre a tarefa!'
        }
    },
    methods: {
        async setTaskDesc() {
            if(this.task_desc_data != null){
                const dataJson = JSON.stringify({descricao: this.task_desc_data})
    
                const req = await fetch(`http://localhost:3000/tarefas/${this.task_id}`, {
                    method: "PATCH",
                    headers: {'Content-Type' : 'application/json'},
                    body: dataJson
                })

                alert('descrição salva!')

            }else alert('bota a descrição ai')

        }
    }
}
</script>

<style scoped>
    #task-details-header{
        display: flex;
        align-items: center;
        width: 100%;
        margin-bottom: 50px;
    }
    #task-details-header h1{
        margin-left: 20px;
    }
    #task-details-text{
        resize: none;
        width: 500px;
        padding: 10px;
        border: none;
        margin-top: 10px;
        margin-bottom: 30px;
    }
</style>