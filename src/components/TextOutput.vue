<template>
    <div>
        <h2>変換後テキスト</h2>
        <textarea :value="outputText" rows="6" readonly></textarea>
    </div>
</template>

<script setup>
defineProps(['outputText'])
</script>

<style scoped>
textarea {
width: 100%;
margin: 12px 0;
padding: 8px;
}
</style>
  