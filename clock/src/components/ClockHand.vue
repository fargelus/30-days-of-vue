<template>
  <div class="hand" :class="{ second: isSecond }"></div>
</template>

<script>
export default {
  name: "ClockHand",
  props: {
    timeValue: Number,
    offsetDegrees: Number,
    class: String,
  },

  data() {
    return {
      initialRotate: this.$props.offsetDegrees,
      isSecond: this.$props.class === "second",
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

.hand.second {
  background: #891313;
}
</style>
