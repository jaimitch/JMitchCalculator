<template>
  <div class="calculator">

<div class="display">{{current || 0}}</div>
<div @click="leftP" class="leftP btn">(</div>
<div @click="rightP" class="rightP btn">)</div>
<div @click="clear" class="btn">C</div>
<div @click="plusMinus" class="btn">+/-</div>
<div @click="percentage" class="btn">%</div>
<div @click="quotient" class="btn operator">/</div>
<div @click="append(7)" class="btn">7</div>
<div @click="append(8)" class="btn">8</div>
<div @click="append(9)" class="btn">9</div>
<div @click="product" class="btn operator">x</div>
<div @click="append(4)" class="btn">4</div>
<div @click="append(5)" class="btn">5</div>
<div @click="append(6)" class="btn">6</div>
<div @click="difference" class="btn operator">-</div>
<div @click="append(1)" class="btn">1</div>
<div @click="append(2)" class="btn">2</div>
<div @click="append(3)" class="btn">3</div>
<div @click="sum" class="btn operator">+</div>
<div @click="append(0)" class="btn zero">0</div>
<div @click="point()" class="btn">.</div>
<div @click="equal" class="btn operator">=</div>


  </div>
</template>

<script>
export default {
data() {
  return {
    previous: null,
    current: '',
    operator: null,
    operatorClicked: false,
  }
},
methods: {
  clear() {
    this.current = '';
  },
  plusMinus() {
    this.current = this.current.charAt(0) === '-' ?
    this.current.slice(1) : `-${this.current}`;
  },
  percentage() {
    this.current = `${parseFloat(this.current) / 100}`;
  },
  append(number) {
    if (this.operatorClicked) {
      this.current = '';
      this.operatorClicked = false;
    }
    this.current = `${this.current}${number}`;
  },
  point() {
    if (this.current.indexOf('.') === -1) {
      this.append('.')
    }
  },
  leftP() {
    if (this.current.indexOf('(') === -1) {
      this.append('(')
    }
  },
  rightP() {
    if (this.current.indexOf(')') === -1) {
      this.append(')')
    }
  },
  setPrevious() {
    this.previous = this.current;
    this.operatorClicked = true;
  },
  quotient() {
    this.operator = (a, b) => a / b;
    this.setPrevious();
  },
  product() {
    this.operator = (a, b) => a * b;
    this.setPrevious();
  },
  difference() {
    this.operator = (a, b) => a - b;
    this.setPrevious();
  },
  sum() {
    this.operator = (a, b) => a + b;
    this.setPrevious();
  },
  equal() {
    this.current = `${this.operator(
      parseFloat(this.current),
      parseFloat(this.previous)
    )}`;
    this.previous = null;
  }
}
}
</script>


<style scoped>
.calculator {
margin: 0 auto;
width: 400px;
font-size: 40px;
display: grid;
grid-template-columns: repeat (4, 1fr);
grid-auto-rows: minmx(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background: black;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.leftP {
  grid-column: 1 / 3;
}
.rightP {
  grid-column: 3 / 5;
}

.btn {
  background-color: #eee;
  border: 1px solid #333;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
