<template>
  <h1>師大 GPA 計算機</h1>
  <calculator></calculator>
  <footer>
      <p>Created by Lapor  <a href="https://github.com/laporchen/gpa-calculator"><i class="fa-brands fa-github"></i></a></p>
  </footer>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  },
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
