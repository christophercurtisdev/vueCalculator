<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear()" class="btn">C</div>
    <div @click="sign()" class="btn">+/-</div>
    <div @click="percent()" class="btn">%</div>
    <div @click="add()" class="btn operator">+</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="subtract()" class="btn operator">-</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="multiply()" class="btn operator">*</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="divide()" class="btn operator">/</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot()" class="btn">.</div>
    <div @click="equals()" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: null
    };
  },
  methods: {
    clear() {
      this.current = "";
      this.operator = null;
      this.previous = "";
    },

    sign() {
      this.current = `${parseFloat(this.current) * -1}`;
    },

    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },

    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },

    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },

    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },

    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },

    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },

    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },

    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },

    equals() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 300px;
  font-size: xx-large;
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

.btn {
  background-color: #eee;
  border: solid 1px #bbb;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
