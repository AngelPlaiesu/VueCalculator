<script setup>
import { ref } from 'vue';

const result = ref('');
const reversedNum = num => parseFloat(num.toString().split('').reverse().join('')) * Math.sign(num)

const ifOperator = (value) => {
  return value === '+' || value === '-' || value === '*' || value === '/';
};

const typeInInput = (value) => {

  if (value === 'AC') {
    result.value = '';
    return;
  }
  if (value === '%') {
    result.value = (parseFloat(result.value) / 100).toString();
    return;
  }
  if (value === '=') {
    try {
      result.value = eval(result.value).toString();
    } catch (error) {

    }

    return;
  }
  if (value === '<') {
    result.value = result.value.slice(0, -1);
    return;
  }
  if (value === ',') {
    result.value += '.';
    return
  }

  if (ifOperator(value)) {
    if (ifOperator(result.value[result.value.length - 1])) {
      result.value = result.value.slice(0, -1) + value;
      return;
    }
  }

  result.value += value;
};



</script>

<template>
  <main>
    <div class="container h-screen mx-auto flex items-center justify-center">
      <div class="grid grid-cols-1 gap-4 ">
        <input class="bg-teal-900 w-[20vw] h-[5vw] rounded-md text-right p-4 text-3xl" v-model="result" disabled />

        <div class="grid grid-cols-4 w-[20vw] h-[25vw] gap-2">
          <button v-for="item in ['AC', '%', '/', '<', 7, 8, 9, '*', 4, 5, 6, '-', 1, 2, 3, '+', 0, ',', '=']"
            :key="item.id" class="w-full h-full bg-red-800 rounded-md" :class="{
              'col-span-2': item === '=',
            }" @click="typeInInput(item)">
            {{ item }}
          </button>
        </div>
      </div>
    </div>
  </main>
</template>
