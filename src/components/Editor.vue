<script setup lang="ts">

  import { ref, defineEmit } from 'vue';

  const emit = defineEmits<{
    (e: 'send', message: string): void
  }>();

  const newMessage = ref<string>('');

  const onEdit = (e) => {
    const keyCode = e.which || e.keyCode;

    // 13 represents the Enter key
    if (keyCode === 13 && !e.shiftKey) {
      // Don't generate a new line
      e.preventDefault();
      // console.log(e);
      // Send message
      console.log(newMessage.value);
      emit('send', newMessage.value);
      newMessage.value = '';
    }
    
  };

</script>

<template>
<main class="editor-frame">
  <textarea @keydown="onEdit" v-model="newMessage"></textarea>
</main>
</template>

<style lang="css" scoped>

.editor-frame {
  width: 100%;
  height: 200px;
  padding: 30px;
}

.editor-frame > textarea {
  width: 100%;
  height: 100%;
  padding: 3px;
  background-color: var(--background);
  color: var(--secondary);
  font-size: 16px;
  resize: none;
}
  
</style>
