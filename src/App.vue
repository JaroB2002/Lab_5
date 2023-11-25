<script setup>
import VideoPlayer from './components/Video/VideoPlayer.vue';
import VideoDetails from './components/Video/VideoDetails.vue';
import Chat from './components/Chat/Chat.vue';
import { ref } from 'vue';


let newDiscription = ref("Default title");

const updateVideo = (description) => {
  newDiscription.value = description;
}

</script>

<template>
  <div class="tiktok">
    <div>
      <VideoPlayer @update:video-description="updateVideo"/>
    </div>
    <div>
      <VideoDetails :description="newDiscription" />
      <Chat />
    </div>
  </div>
</template>

<style scoped>
  .tiktok{
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>
