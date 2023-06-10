<template>
  <timezone-picker></timezone-picker>
  <analog-clock></analog-clock>
</template>

<script>
import AnalogClock from "./components/AnalogClock.vue";
import TimezonePicker from "./components/TimezonePicker.vue";

export default {
  name: "App",
  components: {
    AnalogClock,
    TimezonePicker,
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
