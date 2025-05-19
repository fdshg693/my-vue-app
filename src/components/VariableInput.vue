<template>
    <div>
        <h2>変数ペア入力</h2>
        <VariablePair v-for="(pair, index) in pairs" :key="index" :pair="pair" />
        <button @click="addPair">＋ 追加</button>
    </div>
</template>

<script setup>
import VariablePair from './VariablePair.vue'
defineProps(['pairs', 'addPair'])
</script>
