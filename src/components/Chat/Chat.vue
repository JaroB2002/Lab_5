<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue'; //enkel importeren wat je nodig hebt, houdt de opslag klein
    let message = ref(''); //ref is een reactieve variabele, voor simpele variabelen als int - string - boolean, reflection = iets in het oog houden
    let allMessages = reactive({
        data: [],
    }); //reactive is voor complexe variabelen als arrays en objecten

    onMounted(async () => {
    try {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data;
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
        body: JSON.stringify({ text: message.value }),
      });

      if (response.ok) {
        const data = await response.json();
        const newMessage = { id: data.id, text: message.value };
        allMessages.data.push(newMessage);
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

<style scoped>
</style>