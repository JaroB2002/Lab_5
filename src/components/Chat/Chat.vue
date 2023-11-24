<script setup>
    // import ref
    import { ref, reactive, onMounted } from 'vue'

    let message = ref('') // int, string, boolean
    let allMessages = reactive({
        data: ["Heel", "Even", "Simpel", "Doen"],
    });

    // function sendMessage
    const sendMessage = () => {
        allMessages.data.push(message.value)
        message.value = '' // value van de reflective variabele
    }

</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data">{{ m }}</li>
    </ul>

    <div>
        <input v-model="message" type="text" placeholder="type your message here">
        <button @click="sendMessage">Send</button>
    </div>
  </div>
</template>

<style>

</style>