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
  background: #018ded url(https://unsplash.it/1500/1000?image=881&blur=5);
  background-size: cover;
  font-family: "helvetica neue";
  text-align: center;
  font-size: 10px;
}
</style>
