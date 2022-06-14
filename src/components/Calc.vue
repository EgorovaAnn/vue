<template>
  <div>
    <div class="main">
      <label for="op1">
        <input id="op1" type="number" v-model.number="op1">
      </label>
      <label for="op2">
        <input id="op2" type="number" v-model.number="op2">
      </label>
      = {{ result }} <br/>
      Fibonacci = {{ fibResult }}
    </div>
    <div v-if="error">
      {{ error }}
    </div>
    <!--    <div v-show="error">-->
    <!--      {{ error }}-->
    <!--    </div>-->
    <!--    <div>-->
    <!--      <button @click="sum">+</button>-->
    <!--      <button @click="sub">-</button>-->
    <!--      <button @click="div">/</button>-->
    <!--      <button @click="mult">*</button>-->
    <!--    </div>-->
    <div class="messages">
      <template v-if="result < 0">Получилось отрицательное число</template>
      <template v-else-if="result < 100">Результат в первой сотне</template>
      <template v-else>Просто условие</template>
    </div>
    <div>
      <button
        v-for="operator of operators"
        :key="operator"
        @click="calculate(operator)"
      >{{ operator }}</button>
    </div>
    <div class="logs">
      {{ logs }}
    </div>
    <div>
      <input
        type="checkbox"
        id="keyboard"
        v-model="checkedKeyboard"
        :checked="checkedKeyboard"
      >
      <label for="keyboard">Отобразить экранную клавиатуру</label>
    </div>
    <div v-show="checkedKeyboard">
    <div>
      <button
        v-for="numeral of numerals"
        :key="numeral"
        @click="clickKeyboard(numeral)"
      >{{ numeral }}</button>
      <button @click="back">Стереть</button>
    </div>
    <div>
      <input
        type="radio"
        id="one"
        value="op1"
        v-model="activeOp"
      >
      <label for="one">Операнд 1</label>
      <input
        type="radio"
        id="two"
        value="op2"
        v-model="activeOp"
      >
      <label for="two">Операнд 2</label>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalcComponent',
  data() {
    return {
      op1: 0,
      op2: 0,
      result: 0,
      fibResult: 0,
      error: '',
      operators: ['+', '-', '/', '*'],
      numerals: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9,],
      logs: {},
      checkedKeyboard: false,
      activeOp: 'op1'
    };
  },
  methods: {
    calculate(operator) {
      this.error = '';
      // eslint-disable-next-line default-case
      switch (operator) {
        case '+': this.sum(); break;
        case '-': this.sub(); break;
        case '/': this.div(); break;
        case '*': this.mult(); break;
      }
      // this.logs[Date.now()] = `${this.op1} ${operator} ${this.op2} = ${this.result}`;
      // const newLog = { [Date.now()]: `${this.op1} ${operator} ${this.op2} = ${this.result}` };
      // this.logs = { ...this.logs, ...newLog };
      // Vue.set();
      this.$set(this.logs, Date.now(), `${this.op1} ${operator} ${this.op2} = ${this.result}`);
    },
    clickKeyboard(numeral) {
      const selectedOp = this[this.activeOp];
      if (typeof selectedOp === 'number') {
        this[this.activeOp] = Number(`${selectedOp}${numeral}`);
      }
    },
    back() {
      const selectedOp = this[this.activeOp];
      if (typeof selectedOp === 'number') {
        this[this.activeOp] = Math.trunc(selectedOp / 10);
      }
    },
    sum() {
      const { op1, op2 } = this;
      this.error = '';
      this.result = op1 + op2;
      // this.fibResult = this.fib(op1) + this.fib(op2);
      this.fibResult = this.fib1 + this.fib2;
    },
    sub() {
      const { op1, op2 } = this;
      this.error = '';
      this.result = op1 - op2;
      // this.fibResult = this.fib(op1) + this.fib(op2);
      this.fibResult = this.fib1 - this.fib2;
    },
    div() {
      const { op1, op2 } = this;
      this.error = '';
      if (this.op2 === 0) {
        this.error = 'На ноль делить нельзя';
        return;
      }
      this.result = op1 / op2;
      // this.fibResult = this.fib(op1) + this.fib(op2);
      this.fibResult = this.fib1 / this.fib2;
    },
    mult() {
      const { op1, op2 } = this;
      this.error = '';
      this.result = op1 * op2;
      // this.fibResult = this.fib(op1) + this.fib(op2);
      this.fibResult = this.fib1 * this.fib2;
    },
    fib(n) {
      console.log('fib');
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },
  },
  computed: {
    fib1() {
      return this.fib(this.op1);
    },
    fib2() {
      return this.fib(this.op2);
    },
  },
};
</script>

<style scoped>

</style>
