<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld :msg="msg"/>
    <p>{{ msg }}</p>
<!--    <button @click="inc(2, $event)">{{ counter }}</button>-->
<!--    <button @click="reset">Reset counter</button>-->
    <input type="text" placeholder="text" v-model="someText">
    <p>{{ someText }}</p>
    <CalcComponent></CalcComponent>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import CalcComponent from './components/Calc.vue';

export default {
  name: 'App',
  data () {
    return {
      msg: 'Hello Vue!',
      counter: 0,
      someText: '',
    }
  },
  methods: {
    inc (step, event) {
      console.log(event),
      this.counter++
    },
    reset () {
      this.counter = 0
    }
  },
  components: {
    HelloWorld,
    CalcComponent,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
