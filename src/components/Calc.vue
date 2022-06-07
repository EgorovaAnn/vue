<template>
  <div>
    <div class="main">
      <input type="number" v-model.number="op1">
      <input type="number" v-model.number="op2">
      = {{ result }}
    </div>
    <div>
      <button @click="result = op1 + op2">+</button>
      <button @click="sub">-</button>
      <button @click="div">/</button>
      <button @click="mult">*</button>
      <button @click="expon">^2</button>
      <button @click="div2">:</button>
    </div>
  </div>

</template>

<script>
export default {
  name: "CalcComponent",
  data() {
    return {
      op1: 0,
      op2: 0,
      result: 0,
    };
  },
  methods: {
    sub() {
      this.result = this.op1 - this.op2;
    },
    div() {
      this.result = this.op1 / this.op2;
    },
    mult() {
      this.result = this.op1 * this.op2;
    },
    expon() {
      this.result = this.op1 * this.op1;
    },
    div2() {
      this.result = parseInt(this.op1/this.op2);
    },
  },
};
</script>

<style scoped>

</style>
