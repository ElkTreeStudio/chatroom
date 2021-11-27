<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { collection, query, where, addDoc, doc, onSnapshot } from "firebase/firestore"; 
import { db } from '../firebase';
import ChatRoom from './ChatRoom.vue';
import Editor from './Editor.vue';

const messagesList = ref<string[]>([]);

const sendMessage = async(message) => {
  console.log('Interface', message);
  const originArray = [...messagesList.value];
  // originArray.push(message);
  // messagesList.value = originArray;
  try {
    const docRef = await addDoc(collection(db, "messages"), {
      message: message,
      time: new Date(),
      to: 'user2',
      from: 'Test'
    });
    console.log("Document written with ID: ", docRef.id);
  } catch (e) {
    console.error("Error adding document: ", e);
  }
};

const receiveMessage = () => {
  const q = query(collection(db, "messages"), where("from", "==", "Test"));
  const unsubscribe = onSnapshot(q, (querySnapshot) => {
    const messages = [];
    querySnapshot.forEach((doc) => {
        messages.push(doc.data().message);
    });
    console.table("Messages: ", messages);
    messagesList.value = messages;
  });
  /* const unsub = onSnapshot(doc(db, "messages", "z9Cttb4gN2lvB7wdx946"), (doc) => {
    console.log("Current data: ", doc.data());
  }); */
};

onMounted(() => {
  receiveMessage();
});

</script>

<template>
<section class="chat-interface-frame">
  <ChatRoom :messageData="messagesList" />
  <Editor @send="sendMessage" />
</section>
</template>

<style lang="css" scoped>

.chat-interface-frame {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-end;
  align-content: flex-end;
  width: 800px;
  height: 1000px;
  border-radius: 50px;
  background: var(--background);
  /* box-shadow:  20px 20px 60px #2b2b2b, -20px -20px 60px #3b3b3b; */
}
  
</style>