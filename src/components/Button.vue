<template>
    <input type="submit" id="task-btn" :value="msg">
</template>

<script>
export default {
    name: 'Button',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    #task-btn{
        width: auto;
        padding: 10px;
        border: 1px solid whitesmoke;
        background-color: whitesmoke;
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