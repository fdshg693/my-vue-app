<template>
    <div>
        <h2>変換前テキスト</h2>
        <p>変数名を{}で囲うのを忘れずに！！</p>
        <textarea
      :value="inputText"
      @input="$emit('update:inputText', $event.target.value)"
      rows="6"
      placeholder="ここに {変数} を含むテキストを入力..."
    ></textarea>
        <button @click="convertText">🔄 変換</button>
    </div>
</template>

<script setup>
defineProps(['inputText', 'convertText'])
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
  