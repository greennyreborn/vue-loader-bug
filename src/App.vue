<template>
  <div id="app">
    <test></test>
  </div>
</template>

<script>
import test from './components/test.vue'
console.dir(test.name)

export default {
  components: {
    test
  }
}
</script>

<style>
body {
  font-family: Helvetica, sans-serif;
}
.test {
  /* visibility: hidden; */
}
</style>
