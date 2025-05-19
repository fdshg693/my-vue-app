<template>
    <div>
        <div>
            <textarea :value="beforeOrderText" @input="$emit('update:beforeOrderText', $event.target.value)"
                placeholder="順序付け前のテキストを入力"></textarea>
            <button @click="convertToOrderedText">順序付け</button>
        </div>
        <div>
            <label>順序付け後:</label>
            <textarea readonly>{{ afterOrderText }}</textarea>
        </div>
    </div>
</template>

<script setup>
import { toRefs } from 'vue'
const props = defineProps({
    beforeOrderText: String,
    afterOrderText: String,
    convertToOrderedText: Function
})
const { beforeOrderText, afterOrderText, convertToOrderedText } = toRefs(props)
</script>

<style scoped>
textarea {
    width: 100%;
    min-height: 60px;
    margin-bottom: 8px;
}
</style>
