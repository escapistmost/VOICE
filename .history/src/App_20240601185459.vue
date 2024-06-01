<template>
  <div id="app">
    <div id="particles-js"></div>
    <VoiceGenerator />
  </div>
</template>

<script>
import VoiceGenerator from './components/VoiceGenerator.vue';

export default {
  name: 'App',
  components: {
    VoiceGenerator
  },
  mounted() {
    particlesJS.load('particles-js', '/particles.json', function() {
      console.log('particles.js loaded - callback');
    });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f5f5f5;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
