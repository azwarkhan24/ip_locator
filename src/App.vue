<template>
  <div id="app">
    <ipTracker></ipTracker>
  </div>
</template>

<script>
import ipTracker from './components/ipTracker.vue';

export default {
  name: 'App',
  components: {
    ipTracker
  }
}
</script>

<style>
#app {
  background-color: grey;
  height: 200vh;
}
::-webkit-scrollbar{
  width: 0;
}

</style>
