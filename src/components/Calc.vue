<template>
  <div class="calculadora">
    <div v-html="currentVal" ref="myDiv" class="display"></div>
    <div v-on:click="clear()" class="botao">C</div>
    <div class="botao">+/-</div>
    <div class="botao">%</div>
    <div class="botao operadores">÷</div>
    <div v-on:click="show(7)" class="botao">7</div>
    <div v-on:click="show(8)" class="botao">8</div>
    <div v-on:click="show(9)" class="botao">9</div>
    <div v-on:click="show2('*')" class="botao operadores">x</div>
    <div v-on:click="show(4)" class="botao">4</div>
    <div v-on:click="show(5)" class="botao">5</div>
    <div v-on:click="show(6)" class="botao">6</div>
    <div class="botao operadores">-</div>
    <div v-on:click="show(1)" class="botao">1</div>
    <div v-on:click="show(2)" class="botao">2</div>
    <div v-on:click="show(3)" class="botao">3</div>
    <div v-on:click="show2('+')" class="botao operadores">+</div>
    <div v-on:click="show(0)" class="botao zero">0</div>
    <div v-on:click="show('.')" class="botao">.</div>
    <div v-on:click="calc()" class="botao">=</div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      currentVal: "",
      first: "",
      second: "",
      param: 0,
      operation: "",
    };
  },
  methods: {
    show(value) {
      if (this.param == 0) {
        value = value.toString();
        this.first += value;
        this.currentVal += value;
      } else {
        value = value.toString();
        this.second += value;
        this.currentVal += value;
      }
    },
    show2(operator) {
      this.param = 1;
      this.currentVal += operator;
      this.operation = operator;
    },
    calc() {
      switch (this.operation) {
        case "+": {
          this.currentVal = parseFloat(this.first) + parseFloat(this.second);
          this.first = this.currentVal.toString();
          this.second = "";
          break;
        }
        case "*": {
          this.currentVal = parseFloat(this.first) * parseFloat(this.second);
          this.first = this.currentVal.toString();
          this.second = "";
          break;
        }
        default:
      }
    },
    clear() {
      this.currentVal = "";
      this.first = "";
      this.second = "";
      this.param = 0;
      this.operation = "";
    },
  },
};
</script>



<style scoped>
.calculadora {
  margin: 0 auto;
  width: 350px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1 / 3;
}
.botao {
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operadores {
  background-color: orange;
  color: white;
}
.operadores:hover {
  cursor: pointer;
}
</style>
