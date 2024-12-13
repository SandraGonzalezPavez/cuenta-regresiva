<script>
import CountdownTimer from './components/CountdownTimer.vue';

export default {
  components: {
    CountdownTimer,
  },
};
</script>

<template>
  <div id="app">
  
    <CountdownTimer />
  </div>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
 border-style: double;
  text-align: center;
  background-color: rgb(130, 164, 228);
  color: #080909;
  margin-top: 60px;
}
</style>
