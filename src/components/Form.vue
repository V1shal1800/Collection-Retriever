<template>
    <header>
        <form v-on:submit="onSubmit()" v-on:submit.prevent="send">
            <label for="postman-key-input">Enter Postman Key:</label>
            <input type="text" id="pkin" name="postman-key-input">
            <button type="submit">Fetch</button>
        </form>
    </header>
</template>

<script>
export default {
    name: 'Form',
    methods: {
        onSubmit() {
            const value = document.querySelector("#pkin").value
            document.querySelector("#pkin").value = ""
            this.$emit('key-submitted',value)
        },
    },
}
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
    button{
        padding: 3px 5px;
        margin: 5px;
        border-radius: 4px;
        background-color: white;
        color: black;
        border: 2px solid black;
        transition-duration: 0.4s;
    }
    label{
        margin: 2px;
    }
    button:hover{
        background-color: black;
        color: white;
    }
    input[type=text],input[type=text]:focus  {
        width: 100%;
        border: none;
        border-bottom: 2px solid black;
    }
</style>