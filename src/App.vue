<script setup>
import VideoPlayer from './components/Video/VideoPlayer.vue'
import VideoDetails from './components/Video/VideoDetails.vue'
import Chat from './components/Chat/Chat.vue'

import { ref } from 'vue';
let newDescription = ref("Default title");
const updateVideo = (description) => {
  console.log(description);
  newDescription.value = description;
}


</script>

<template>
  <div class="tiktok">
    <div>
      <div><VideoPlayer @update:video-description="updateVideo"/></div>
    </div>
    <div>
      <Chat/>
      <VideoDetails :description="newDescription"/>
    </div>

  </div>
</template>

<style scoped>
  .tiktok {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>