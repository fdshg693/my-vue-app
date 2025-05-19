<template>
  <div class="app">
    <select v-model="selectedComponent">
      <option disabled value="">追加するコンポーネントを選択</option>
      <option v-for="option in options" :key="option.value" :value="option.value"
        :disabled="addedComponents.includes(option.value)" :class="{ selected: selectedComponent === option.value }">
        {{ option.label }}
      </option>
    </select>
    <button @click="addComponent" :disabled="!selectedComponent">追加</button>

    <component v-for="(item, idx) in addedComponents" :is="componentMap[item]" :key="idx" v-bind="getProps(item)"
      v-model:pairs="pairs" v-model:inputText="inputText" v-model:beforeOrderText="beforeOrderText" :addPair="addPair"
      :convertText="convertText" :convertToOrderedText="convertToOrderedText" :outputText="outputText"
      :afterOrderText="afterOrderText" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import VariableInput from './components/VariableInput.vue'
import TextInOut from './components/TextInOut.vue'
import OrderTextInOut from './components/OrderTextInOut.vue'

// コンポーネント名と実体のマッピング
const componentMap = {
  VariableInput,
  TextInOut,
  OrderTextInOut,
}

const pairs = ref([{ key: '', value: '' }])
const inputText = ref('')
const outputText = ref('')
const beforeOrderText = ref('')
const afterOrderText = ref('')

const selectedComponent = ref('')
const addedComponents = ref([])

// ドロップダウンの選択肢リスト
const options = [
  { value: 'VariableInput', label: '変数入力' },
  { value: 'TextInOut', label: 'テキスト入力・出力' },
  { value: 'OrderTextInOut', label: '順序付きテキスト' },
]

function addPair() {
  pairs.value.push({ key: '', value: '' })
}

function convertText() {
  let result = inputText.value
  for (const { key, value } of pairs.value) {
    if (key) {
      const regex = new RegExp(`\\{${key}\\}`, 'g')
      result = result.replace(regex, value)
    }
  }
  outputText.value = result
}

function convertToOrderedText() {
  const lines = beforeOrderText.value.split('\n')
  const orderedLines = lines.map((line, index) => `${index + 1}. ${line}`)
  afterOrderText.value = orderedLines.join('\n')
}

function addComponent() {
  if (selectedComponent.value) {
    addedComponents.value.push(selectedComponent.value)
    selectedComponent.value = ''
  }
}

// 各コンポーネントに必要なpropsだけ渡す
function getProps(name) {
  switch (name) {
    case 'VariableInput':
      return { pairs: pairs.value, addPair }
    case 'TextInOut':
      return { inputText: inputText.value, outputText: outputText.value, convertText }
    case 'OrderTextInOut':
      return { beforeOrderText: beforeOrderText.value, afterOrderText: afterOrderText.value, convertToOrderedText }
    default:
      return {}
  }
}
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: auto;
  font-family: sans-serif;
}

select option.selected {
  background: #2196f3;
  color: #fff;
}

select option:disabled {
  color: #aaa;
  background: #f0f0f0;
}
</style>
