<script setup lang="ts">
import { ref } from 'vue';
import Editor from './Editor.vue';

const messagesList = ref<string[]>([]);

const sendMessage = (message) => {
  console.log('Interface', message);
  const originArray = [...messagesList.value];
  originArray.push(message);
  messagesList.value = originArray;
  console.log(messagesList);
};

</script>

<template>
<section class="chat-interface-frame">
  <div v-for="(msg, idx) in messagesList" :key="idx">
    {{ msg }}
  </div>
  <Editor @send="sendMessage" />
</section>
</template>

<style lang="css" scoped>

.chat-interface-frame {
  display: flex;
  align-items: flex-end;
  align-content: flex-end;
  width: 800px;
  height: 1000px;
  border-radius: 50px;
  background: var(--background);
  /* box-shadow:  20px 20px 60px #2b2b2b, -20px -20px 60px #3b3b3b; */
}
  
</style>