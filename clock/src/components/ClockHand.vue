<template>
  <div class="hand"></div>
</template>

<script>
export default {
  name: "ClockHand",
  props: {
    timeValue: Number,
    offsetDegrees: Number,
  },

  data() {
    return {
      initialRotate: this.$props.offsetDegrees,
    };
  },

  computed: {
    rotateValue() {
      return this.initialRotate + this.$props.timeValue * 6;
    },

    rotateProperty() {
      return `rotate(${this.rotateValue}deg)`;
    },
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
  transform: v-bind(rotateProperty);
}
</style>
