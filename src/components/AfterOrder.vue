<template>
    <div>
        <h2>変換後テキスト</h2>
        <p>順序付き</p>
        <textarea :value="afterOrderText" rows="6" readonly></textarea>
    </div>
</template>

<script setup>
defineProps(['afterOrderText'])
</script>

<style scoped>
textarea {
width: 100%;
margin: 12px 0;
padding: 8px;
}
</style>
  