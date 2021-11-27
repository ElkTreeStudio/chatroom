<script setup lang="ts">

interface PropsData {
  messageData: string[]
}

import { defineProps, toRefs } from 'vue';

const props = defineProps<PropsData>();
const { messageData } = toRefs(props);


const checkData = () => {
  console.log(messageData);
};

</script>

<template>
  <main class="chatroom-frame">
    <div v-for="(msg, idx) in messageData" :key="idx">
      <p v-html="msg"></p>
    </div>
  </main>

</template>

<style lang="css" scoped>

.chatroom-frame {
  width: 100%;
  height: auto;
  padding: 30px;
}

</style>
