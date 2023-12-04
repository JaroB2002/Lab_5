<script setup>
import { ref, reactive, onMounted } from 'vue';

let message = ref('');
let allMessages = reactive({
    data: [],
});

onMounted(async () => {
    try {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data.reverse().slice(0, 16); // Omgekeerde volgorde en maximaal 16 berichten
    } catch (error) {
        console.error(error);
    }
});

const sendMessage = async () => {
    try {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ text: message.value, user: 'Jaro Brichau'}),

            
        });

        if (response.ok) {
            const data = await response.json();
            const newMessage = { id: data.id, text: message.value };
            allMessages.data = [newMessage, ...allMessages.data.slice(0, 15)]; // Voeg het nieuwe bericht toe en behoud maximaal 16 berichten
            message.value = '';
        } else {
            console.error('Msg failed to send');
        }
    } catch (error) {
        console.error(error);
    }
};
</script>

<template>
  <div>
    <ul>
      <li v-for="m in allMessages.data" :key="m.id">
        {{ m.text }}
      </li>
    </ul>
    <div>
      <input v-model="message" type="text" placeholder=""> 
      <button @click="sendMessage">Send</button> 
    </div>
  </div>
</template>
