<script setup lang="ts">

import { ref } from 'vue';

const userName = ref<string>('');

const onClick = () => {
  userName.value = 'Name';
};

</script>

<template>
  <button @click="onClick">Click me</button>
  <h1>{{ userName }}</h1>
</template>
