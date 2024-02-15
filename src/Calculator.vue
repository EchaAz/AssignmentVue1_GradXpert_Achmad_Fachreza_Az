<template>
    <div id="calculator">
      <div class="display">{{ display }}</div>
      <div class="buttons">
        <button @click="clear">C</button>
        <button @click="backspace">←</button>
        <button @click="appendSymbol('+')">+</button>
        <button @click="appendSymbol('-')">-</button>
        <button @click="appendNumber(1)">1</button>
        <button @click="appendNumber(2)">2</button>
        <button @click="appendNumber(3)">3</button>
        <button @click="appendSymbol('*')">*</button>
        <button @click="appendNumber(4)">4</button>
        <button @click="appendNumber(5)">5</button>
        <button @click="appendNumber(6)">6</button>
        <button @click="appendSymbol('/')">/</button>
        <button @click="appendNumber(7)">7</button>
        <button @click="appendNumber(8)">8</button>
        <button @click="appendNumber(9)">9</button>
        <button @click="calculateResult">=</button>
        <button @click="appendNumber(0)">0</button>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue';
  
  export default {
    setup() {
      const display = ref('0');
      const operand1 = ref('');
      const operand2 = ref('');
      const operator = ref('');
      const result = ref('');
  
      const clear = () => {
        display.value = '0';
        operand1.value = '';
        operand2.value = '';
        operator.value = '';
        result.value = '';
      };
  
      const backspace = () => {
        display.value = display.value.slice(0, -1);
      };
  
      const appendSymbol = (symbol) => {
        if (display.value === '0' && symbol !== '-') {
          return;
        }
        if (display.value.slice(-1) === '/' && symbol === '*') {
          display.value = display.value.slice(0, -1) + symbol;
        } else {
          display.value += symbol;
        }
      };
  
      const appendNumber = (number) => {
        if (result.value !== '') {
          display.value = '';
          result.value = '';
        }
        if (display.value === '0') {
          display.value = '';
        }
        display.value += number;
      };
  
      const calculateResult = () => {
        try {
          result.value = eval(display.value);
          display.value = result.value.toString();
        } catch (error) {
          display.value = 'Error';
        }
      };
  
      return {
        display,
        clear,
        backspace,
        appendSymbol,
        appendNumber,
        calculateResult
      };
    }
  };
  </script>
  
  <style scoped>
  #calculator {
    width: 200px;
    margin: 20px auto;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 10px;
    background-color: #f5f5f5;
  }
  
  .display {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
    text-align: right;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 5px;
  }
  
  button {
    padding: 10px;
    border: none;
    border-radius: 5px;
    background-color: #e0e0e0;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #ccc;
  }
  </style>
  