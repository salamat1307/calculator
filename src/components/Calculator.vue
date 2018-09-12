<template>
  <div class="calculator">
    <div class="display">{{ result || 0 }}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">$</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiple" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
    data () {
      return {
        previous: null,
        result: '',
        operator: null,
        operatorClicked: false
      }
    },

    methods: {
      clear: function() {
        this.result = '';
      },

      sign: function() {
        this.result = this.result.charAt(0) === '-' ? this.result.slice(1) : `-${this.result}`;
      },
      
      percent: function() {
        this.result = `${parseFloat(this.result) / 100}`
      },

      append: function(number) {
        if(this.operatorClicked) {
          this.result = '';
          this.operatorClicked = false;
        }
        this.result = `${this.result}${number}`;
      },

      dot: function() {
        if(this.result.indexOf('.') === -1) {
          this.append('.');
        }
      },

      divide: function() {
        this.operator = (a, b) => a / b;
        this.previous = this.result;
        this.operatorClicked = true;
      },

      multiple: function() {
        this.operator = (a, b) => a * b;
        this.previous = this.result;
        this.operatorClicked = true;
      },

      minus: function() {
        this.operator = (a, b) => a - b;
        this.previous = this.result;
        this.operatorClicked = true;
      },

      add: function() {
        this.operator = (a, b) => a + b;
        this.previous = this.result;
        this.operatorClicked = true;
      },

      equal: function() {
          this.result = `${this.operator(parseFloat(this.result), parseFloat(this.previous))}`;
          this.previous = null;
      }

    }
}
</script>

<style scoped>
  .calculator {
    width: 500px;
    margin: 0 auto;
    display: grid;
    font-size: 40px;
    text-align: center;
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

  .btn {
    background-color: #F2F2F2;
    border: 1px solid #999; 
  }

  .operator {
    background-color: orange; 
    color: white;
  }
</style>

