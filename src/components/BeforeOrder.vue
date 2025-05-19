<template>
    <div>
        <h2>変換前テキスト</h2>
        <p>順序付き</p>
        <textarea
      :value="beforeOrderText"
      @input="$emit('update:beforeOrderText', $event.target.value)"
      rows="6"
      placeholder=""
    ></textarea>
        <button @click="convertToOrderedText">🔄 変換</button>
    </div>
</template>

<script setup>
defineProps(['beforeOrderText', 'convertToOrderedText'])
</script>

<style scoped>
textarea {
width: 100%;
margin: 12px 0;
padding: 8px;
}
button {
padding: 6px 12px;
margin-top: 10px;
}
</style>
  