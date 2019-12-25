<template>
  <div class="calculator">
    <p>this is the inner test</p>
    <div class="display">{{current || "0"}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="multiply">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="minus">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      operator: null,
      previous: null,
      operatorClicked: false,
      current: ""
    };
  },
  methods: {
    clear: function() {
      this.current = "";
    },
    sign: function() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent: function() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append: function(num) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    dot: function() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious: function() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide: function() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply: function() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus: function() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add: function() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal: function() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 300px;
  margin: 0 auto;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: minmax(40px, auto);
}
.display {
  grid-column: 1/5;
  background-color: #3e3e3e;
  color: white;
}
.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #eee;
  border: 1px solid lightgray;
}

.operator {
  background-color: orange;
}
</style>
