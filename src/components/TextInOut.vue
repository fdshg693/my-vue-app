<template>
    <div>
        <div>
            <textarea :value="inputText" @input="$emit('update:inputText', $event.target.value)"
                placeholder="テキストを入力"></textarea>
            <button @click="convertText">変換</button>
        </div>
        <div>
            <label>出力:</label>
            <textarea>{{ outputText }}</textarea>
        </div>
    </div>
</template>

<script setup>
import { toRefs } from 'vue'
const props = defineProps({
    inputText: String,
    outputText: String,
    convertText: Function
})
const { inputText, outputText, convertText } = toRefs(props)
</script>

<style scoped>
textarea {
    width: 100%;
    min-height: 60px;
    margin-bottom: 8px;
}
</style>
