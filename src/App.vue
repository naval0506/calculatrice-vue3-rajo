<template>
  <div class="container">
    <div class="display">
      <input id="screen" type="text" placeholder="0" v-model="screen" @keydown.enter="evalExpression" ref="screen">
    </div>
    <div class="btns">
      <div class="row">
        <button id="ce" @click="backspace">CE</button>
        <button @click="calculate('factorial')">x!</button>
        <button class="btn" @click="appendToScreen('(')">(</button>
        <button class="btn" @click="appendToScreen(')')">)</button>
        <button class="btn" @click="appendToScreen('%')">%</button>
        <button id="ac" @click="clearScreen">AC</button>
      </div>
      <div class="row">
        <button @click="calculate('sin')">sin</button>
        <button @click="calculate('pi')">π</button>
        <button class="btn" @click="appendToScreen('7')">7</button>
        <button class="btn" @click="appendToScreen('8')">8</button>
        <button class="btn" @click="appendToScreen('9')">9</button>
        <button class="btn" @click="appendToScreen('/')">/</button>
      </div>
      <div class="row">
        <button @click="calculate('cos')">cos</button>
        <button @click="calculate('log')">log</button>
        <button class="btn" @click="appendToScreen('4')">4</button>
        <button class="btn" @click="appendToScreen('5')">5</button>
        <button class="btn" @click="appendToScreen('6')">6</button>
        <button class="btn" @click="appendToScreen('*')">*</button>
      </div>
      <div class="row">
        <button @click="calculate('tan')">tan</button>
        <button @click="calculate('sqrt')">√</button>
        <button class="btn" @click="appendToScreen('1')">1</button>
        <button class="btn" @click="appendToScreen('2')">2</button>
        <button class="btn" @click="appendToScreen('3')">3</button>
        <button class="btn" @click="appendToScreen('-')">-</button>
      </div>
      <div class="row">
        <button @click="calculate('e')">e</button>
        <button @click="calculate('pow')">x<sup>y</sup></button>
        <button class="btn" @click="appendToScreen('0')">0</button>
        <button class="btn" @click="appendToScreen('.')">.</button>
        <button id="eval" @click="evalExpression">=</button>
        <button class="btn" @click="appendToScreen('+')">+</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculatrice-vue',
  data() {
    return {
      screen: ''
    };
  },
  methods: {
    clearScreen() {
      this.screen = '';
    },
    backspace() {
      this.screen = this.screen.slice(0, -1);
    },
    appendToScreen(char) {
      this.screen += char;
    },
    calculate(func) {
      let result = '';
      try {
        switch (func) {
          case 'sin':
            result = Math.sin(parseFloat(this.screen)).toString();
            break;
          case 'cos':
            result = Math.cos(parseFloat(this.screen)).toString();
            break;
          case 'tan':
            result = Math.tan(parseFloat(this.screen)).toString();
            break;
          case 'sqrt':
            result = Math.sqrt(parseFloat(this.screen)).toString();
            break;
          case 'log':
            result = Math.log(parseFloat(this.screen)).toString();
            break;
          case 'pi':
            result = Math.PI.toString();
            break;
          case 'e':
            result = Math.E.toString();
            break;
          case 'factorial':
            result = this.factorial(parseInt(this.screen)).toString();
            break;
          case 'pow':
            result = Math.pow(parseFloat(this.screen), 2).toString();
            break;
          default:
            result = 'Invalid operation';
            break;
        }
      } catch (error) {
        result = 'Error';
      }
      this.screen = result;
    },
    factorial(num) {
      let result = 1;
      for (let i = 1; i <= num; i++) {
        result *= i;
      }
      return result;
    },
    evalExpression() {
      try {
        this.screen = eval(this.screen).toString();
      } catch (error) {
        this.screen = 'Error';
      }
    },
    handleKeypress(event) {
      if (event.key === 'Enter') {
        this.evalExpression();
      }
    }
  },
  mounted() {
    this.$refs.screen.addEventListener('keydown', this.handleKeypress);
  },
  beforeUnmount() {
    this.$refs.screen.removeEventListener('keydown', this.handleKeypress);
  }
};
</script>

<style src="@/assets/style.css"></style>