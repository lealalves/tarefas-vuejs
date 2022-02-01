<template>
    <div id="header">
        <h1>MAKE-YOU-TASK</h1>
        <ul>
            <router-link to="/"><li>home</li></router-link>
            <router-link to="/about"><li>sobre</li></router-link>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style scoped>
    #header{
        display: flex;
        align-items: center;
        width: 100%;
        height: 100px;
        padding: 10px;
        background-color: #222;
        color: aliceblue;
    }
    #header h1{
        margin-left: 40px;
    }
    #header ul{
        display: flex;
        list-style: none;
        margin-left: 20px;
    }
    #header li{
        padding: 8px;
        text-decoration: none;
        margin-left: 10px;
        background-color: whitesmoke;
        border: 1px solid rgb(255, 255, 255);
        color: #222;
        cursor: pointer;
        border-radius: 10px;
        transition: .5s;
    }
    #header li:hover{
        color: whitesmoke;
        background-color: transparent;
    }
</style>