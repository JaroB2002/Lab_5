<script setup>
    //import ref, reactive and onMounted from 'vue';
    import { ref, reactive, onMounted } from 'vue';
    //ref -> iets reflecteren naar de frontend
    let message =ref("");//int, string, boolean
    let allMessages = reactive({
        data: [],
    });//array, object

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
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    text: message.value,
                }),
            });
            if(response.ok){
            const data = await response.json();
            allMessages.data.push(data);
            message.value = "";
        }} catch (error) {
            console.error(error);
        }
    };
</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data" :key="m.id">{{ m.text }}</li>
    </ul>
  </div>
  <div>
        <input v-model="message" type="text" placeholder="Type your message here">
        <button @click="sendMessage">Send</button>
   </div>
</template>

<style scoped>

</style>
