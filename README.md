# vue-loader-bug
A project to demonstrate a vue-loader(9.5.2) bug

### What causes *Maximum call stack size exceeded*

I run into a ```Maximum call stack size exceeded``` bug when use a child component whose name is the same as the current component file name.

Here's the code of current component.
>File name: src/components/test.vue

```js
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
```

I use 'test' -- the child component in the single file component whose file name happens to be 'test', too. And it leads to  ```Recursive Component``` behavior which causes ```Maximum call stack size exceeded``` eventually.

---
So I did a little research, and found there was a commit [Provide default for name option(#396)](https://github.com/vuejs/vue-loader/commit/cd358d62497b475188c999e66a6c7c1598fd23bb) in vue-loader 9.5.2. It simply added a feature that **Use the filename to set a component's name option, if one isn't provided. This allows more helpful debugging messages by default**. I believe this causes the problem.

See, I don't provide a name for the current component. According to this commit, vue-loader will name it as the file name (which is 'test' in my case). As a result, this component will invoke itself which is not my intention. I intended to invoke another component called 'test'.

However, I'm not sure if this is a bug. But it does causes some confusion for beginners.
