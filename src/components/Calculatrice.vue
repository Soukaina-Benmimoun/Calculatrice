<template>
  <div class="content">
     <h1>Calculatrice</h1>
     <input type="text" readonly v-model="currentNumber">
     <div>
       <button @click="appendNumber('7')">7</button>
       <button @click="appendNumber('8')">8</button>
       <button @click="appendNumber('9')">9</button>
       <button @click="setOperator('/')">/</button>
     </div>
     <div>
       <button @click="appendNumber('4')">4</button>
       <button @click="appendNumber('5')">5</button>
       <button @click="appendNumber('6')">6</button>
       <button @click="setOperator('*')">*</button>
     </div>
     <div>
       <button @click="appendNumber('1')">1</button>
       <button @click="appendNumber('2')">2</button>
       <button @click="appendNumber('3')">3</button>
       <button @click="setOperator('-')">-</button>
     </div>
     <div>
       <button @click="appendNumber('0')">0</button>
       <button @click="appendNumber('.')">.</button>
       <button @click="setOperator('+')">+</button>
       <button @click="calculate">=</button>
     </div>
     <button style="width: auto; background-color: red;" @click="clear">Effacer</button>
  </div>
 </template>
 
 <script>
 export default {
  data() {
     return {
       currentNumber: '',
       operator: null,
       firstOperand: null,
     };
  },
  methods: {
     appendNumber(number) {
       this.currentNumber += number;
     },
     setOperator(operator) {
       if (this.operator !== null) {
         this.calculate();
       }
       this.operator = operator;
       this.firstOperand = parseFloat(this.currentNumber);
       this.currentNumber = '';
     },
     calculate() {
       let result;
       switch (this.operator) {
         case '+':
           result = this.firstOperand + parseFloat(this.currentNumber);
           break;
         case '-':
           result = this.firstOperand - parseFloat(this.currentNumber);
           break;
         case '*':
           result = this.firstOperand * parseFloat(this.currentNumber);
           break;
         case '/':
           result = this.firstOperand / parseFloat(this.currentNumber);
           break;
         default:
           return;
       }
       this.currentNumber = result.toString();
       this.operator = null;
       this.firstOperand = null;
     },
     clear() {
       this.currentNumber = '';
       this.operator = null;
       this.firstOperand = null;
     },
  },
 };
 </script>
 
 <style>
 .content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 }
 button {
  width: 100px;
  height: 100px;
  font-size: 40px;
  border: none;
  outline: none;
 }
 input {
  width: 400px;
  height: 100px;
  font-size: 40px;
  border: none;
  outline: none;
 }
 button:focus{
  background-color: rgb(225, 225, 225) !important;;
 }
 </style>
 