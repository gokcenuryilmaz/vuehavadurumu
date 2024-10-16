<!-- src/App.vue -->
<template>
  <div id="app">
    <WeatherApp />
  </div>
</template>

<script>
import WeatherApp from './components/WeatherApp.vue';

export default {
  components: {
    WeatherApp,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>