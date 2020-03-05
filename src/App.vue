<template>
  <div id="app">
    <countdown date="2020-03-06 00:00:00"></countdown>
  </div>
</template>

<script>
import Countdown from "./components/Countdown.vue";

export default {
  name: "App",
  components: {
    Countdown
  }
};
</script>

<style lang="scss">
#app {
  align-items: center;
  justify-content: center;
  position: absolute;
  display: flex;
  background-color: #34495e;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>
