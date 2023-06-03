<template>
  <div
    class="hand"
    :class="{ second: isSecond, minute: isMinute, hour: isHour }"
  ></div>
</template>

<script>
export default {
  name: "ClockHand",
  props: {
    degreeValue: Number,
    offsetDegrees: Number,
    class: String,
  },

  data() {
    return {
      initialRotate: this.$props.offsetDegrees,
      isSecond: this.$props.class === "second",
      isMinute: this.$props.class === "minute",
      isHour: this.$props.class === "hour",
      secondColor: "#891313",
    };
  },

  computed: {
    rotateValue() {
      return this.initialRotate + this.$props.degreeValue;
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
  background: v-bind(secondColor);
}

.hand.minute {
  left: -15px;
  width: calc(50% + 15px);
}

.hand.hour {
  width: 45%;
  left: 25px;
}
</style>
