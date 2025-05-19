<template>
  <div class="app">
    <VariableInput v-model:pairs="pairs" :addPair="addPair" />
    <TextInput v-model:inputText="inputText" :convertText="convertText" />
    <TextOutput :outputText="outputText" />
    <BeforeOrder v-model:beforeOrderText="beforeOrderText" :convertToOrderedText="convertToOrderedText" />
    <AfterOrder :afterOrderText="afterOrderText" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import VariableInput from './components/VariableInput.vue'
import TextInput from './components/TextInput.vue'
import TextOutput from './components/TextOutput.vue'
import AfterOrder from './components/AfterOrder.vue'
import BeforeOrder from './components/BeforeOrder.vue'

const pairs = ref([{ key: '', value: '' }])
const inputText = ref('')
const outputText = ref('')
const beforeOrderText = ref('')
const afterOrderText = ref('')

function addPair() {
  pairs.value.push({ key: '', value: '' })
}

function convertText() {
  let result = inputText.value
  for (const { key, value } of pairs.value) {
    if (key) {
      const regex = new RegExp(`\\{${key}\\}`, 'g')
      result = result.replace(regex, value)
      console.log(`Replaced {${key}} with ${value}`)
      console.log(`Current result: ${result}`)
    }
  }
  outputText.value = result
}

function convertToOrderedText() {
  const lines = beforeOrderText.value.split('\n')
  const orderedLines = lines.map((line, index) => `${index + 1}. ${line}`)
  afterOrderText.value = orderedLines.join('\n')
}

</script>

<style scoped>
.app {
  max-width: 600px;
  margin: auto;
  font-family: sans-serif;
}
</style>
