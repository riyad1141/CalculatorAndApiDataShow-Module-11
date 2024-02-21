<script setup>

import {ref} from "vue";

let CalculatorValue = ref('');
let CalculatorElement = ['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'];

let operator = ref(null);
let previousCalculatorValue = ref('');

const action = (n) => {
  if (!isNaN(n) || n === '.') {
    CalculatorValue.value += n + '';
  }

  if (n === 'C') {
    CalculatorValue.value = '';
  }

  if (n === '%') {
    CalculatorValue.value = CalculatorValue.value / 100 + '';
  }

  if (['/', '*', '-', '+'].includes(n)) {
    operator.value = n;
    previousCalculatorValue.value = CalculatorValue.value;
    CalculatorValue.value = '';
  }

  if (n === '=') {
    CalculatorValue.value = eval(
        previousCalculatorValue.value + operator.value + CalculatorValue.value
    );
    previousCalculatorValue.value = '';
    operator.value = null;
  }
};

</script>

<template>
  <h1 class="p-2 m-2">Original Calculator</h1>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{CalculatorValue || 0}}
    </div>
    <div class="row no-gutters">
      <div class="col-3" v-for="n in CalculatorElement" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
             :class="{'bg-vue-green': ['C','*','/','-','+','%','='].includes(n)}"
             @click="action(n)"
        >
          {{n}}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.bg-vue-dark{
  background: #31475e;
}
.hover-class{
  cursor: pointer;
  background: #3D5875;
}
.bg-vue-green{
  background: #3fb984;
}
</style>