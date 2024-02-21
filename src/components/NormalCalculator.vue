<script setup>

import {ref} from "vue";

const operand1 = ref(null);
const operand2 = ref(null);
const operator = ref(null);
const result = ref(null);

function calculate() {
  if (operand1.value !== null && operand2.value !== null && operator.value !== null) {
    switch (operator.value) {
      case '+':
        result.value = operand1.value + operand2.value;
        break;
      case '-':
        result.value = operand1.value - operand2.value;
        break;
      case '*':
        result.value = operand1.value * operand2.value;
        break;
      case '/':
        if (operand2.value === 0) {
          result.value = 'Error: Division by zero';
        } else {
          result.value = operand1.value / operand2.value;
        }
        break;
    }
  } else {
    result.value = 'Error: Please enter all values.';
  }
}
</script>

<template>

  <div class="calculator-container flex flex-col items-center justify-center p-8 bg-gray-100 rounded-md shadow-md">
    <h2 class="text-2xl font-semi-bold mb-4">Awesome Calculator</h2>

    <div class="flex flex-col md:flex-row gap-4 mb-4">
      <input type="number" v-model.number="operand1" class="input input-bordered input-primary w-full md:w-36" placeholder="First Number" />

      <select v-model.number="operator" class="select select-bordered select-primary w-full md:w-20">
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>

      <input type="number" v-model.number="operand2" class="input input-bordered input-primary w-full md:w-36" placeholder="Second Number" />
    </div>

    <button @click="calculate" class="btn btn-primary w-full">Calculate</button>

    <div class="result-text text-primary mt-4" v-if="result">
      Result: {{ result }}
    </div>
  </div>

</template>

<style scoped>

</style>