<template>
  <analog-clock></analog-clock>
</template>

<script>
import AnalogClock from "./components/AnalogClock.vue";

export default {
  name: "App",
  components: {
    AnalogClock,
  },
};
</script>

<style>
.app {
  background: #018ded url("./assets/bg.jpeg");
  background-size: cover;
  font-family: "helvetica neue";
  text-align: center;
  font-size: 10px;
}
</style>
