<template>
  <div>
    <test></test>
  </div>
</template>

<script>
import test from './test/test.vue'
console.dir(test.name)

export default {
  components: {
    test
  }
}
</script>
