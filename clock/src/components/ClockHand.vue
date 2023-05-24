<template>
  <div class="hand"></div>
</template>

<script>
export default {
  name: "ClockHand",
  props: {
    value: Number,
  },

  data() {
    return {
      //rotateDegree:
    };
  },

  mounted() {
    console.log(this.$props);
  },
};
</script>

<style>
.hand {
  width: 50%;
  height: 6px;
  background: black;
  position: absolute;
  top: 50%;
  transform-origin: right;
  transform: rotate(90deg);
}
</style>
