<template>
    <div class="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container{
        color: #000000;
        background-color: aliceblue;
        border: 2px solid black;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;        
    }
</style>