<template>
    <div class="pair">
      <input v-model="pair.key" placeholder="変数名" />
      <input v-model="pair.value" placeholder="値" />
    </div>
  </template>
  
  <script setup>
  defineProps(['pair'])
  </script>
  
  <style scoped>
  .pair {
    margin-bottom: 8px;
  }
  input {
    margin-right: 8px;
    padding: 4px;
  }
  </style>
  