<template>
  <div class="calculator">
    <h1> Calculator</h1>
    <div class="display">
      <input type="text" :value="currentInput" readonly />
    </div>
    <div class="buttons">
      <button @click="appendNumber('7')">7</button>
      <button @click="appendNumber('8')">8</button>
      <button @click="appendNumber('9')">9</button>
      <button @click="setOperation('/')">/</button>
      <button @click="appendNumber('4')">4</button>
      <button @click="appendNumber('5')">5</button>
      <button @click="appendNumber('6')">6</button>
      <button @click="setOperation('*')">*</button>
      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
      <button @click="setOperation('-')">-</button>
      <button @click="appendNumber('0')">0</button>
      <button @click="appendNumber('.')">.</button>
      <button @click="calculate()">=</button>
      <button @click="setOperation('+')">+</button>
      <button @click="clear()">C</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentInput: '',
      previousInput: '',
      operation: '',
    };
  },
  methods: {
    appendNumber(number) {
      this.currentInput += number;
    },
    setOperation(op) {
      if (this.currentInput === '') return;
      if (this.previousInput !== '') {
        this.calculate();
      }
      this.operation = op;
      this.previousInput = this.currentInput;
      this.currentInput = '';
    },
    calculate() {
      if (this.currentInput === '' || this.previousInput === '') return;
      const prev = parseFloat(this.previousInput);
      const curr = parseFloat(this.currentInput);
      let calcResult;

      switch (this.operation) {
        case '+':
          calcResult = prev + curr;
          break;
        case '-':
          calcResult = prev - curr;
          break;
        case '*':
          calcResult = prev * curr;
          break;
        case '/':
          calcResult = prev / curr;
          break;
        default:
          return;
      }

      this.currentInput = calcResult.toString();
      this.previousInput = '';
      this.operation = '';
    },
    clear() {
      this.currentInput = '';
      this.previousInput = '';
      this.operation = '';
    },
  },
};
</script>

<style>
.calculator {
  max-width: 320px;
  margin: 50px auto;
  padding: 20px;
  border-radius: 10px;
  background: #f4f4f4;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.display {
  background: #fff;
  border-radius: 5px;
  margin-bottom: 20px;
  padding: 10px;
  text-align: right;
  border: 1px solid #ddd;
}

input {
  width: 100%;
  border: none;
  background: #fff;
  font-size: 2em;
  text-align: right;
  outline: none;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  background: #fff;
  border: 1px solid #ddd;
  padding: 20px;
  font-size: 1.2em;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.3s, box-shadow 0.3s;
}

button:hover {
  background: #f0f0f0;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

button:active {
  background: #e0e0e0;
}
</style>
