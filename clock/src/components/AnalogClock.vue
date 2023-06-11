<template>
  <timezone-picker @hours-changed="onHoursChanged"></timezone-picker>

  <div class="clock">
    <div class="clock-face">
      <clock-hand
        class="second"
        :offset-degrees="90"
        :degree-value="secondsDegrees"
      ></clock-hand>
      <clock-hand
        class="minute"
        :offset-degrees="90"
        :degree-value="minutesDegrees"
      ></clock-hand>
      <clock-hand
        class="hour"
        :offset-degrees="90"
        :degree-value="hoursDegrees"
      >
      </clock-hand>
    </div>
  </div>
</template>

<script>
import ClockHand from "./ClockHand.vue";
import TimezonePicker from "./TimezonePicker.vue";

export default {
  name: "AnalogClock",
  components: {
    ClockHand,
    TimezonePicker,
  },

  data() {
    return {
      seconds: this.getCurrentSeconds(),
      minutes: this.getCurrentMinutes(),
      hours: this.getCurrentHours(),
    };
  },

  computed: {
    hoursDegrees() {
      return this.hours * 30;
    },

    minutesDegrees() {
      return this.minutes * 6;
    },

    secondsDegrees() {
      return this.seconds * 6;
    },
  },

  methods: {
    getCurrentSeconds() {
      return new Date().getSeconds();
    },

    getCurrentMinutes() {
      return new Date().getMinutes();
    },

    getCurrentHours() {
      return new Date().getHours();
    },

    onHoursChanged(hours) {
      this.hours = hours;
    },
  },

  mounted() {
    setInterval(() => {
      this.seconds = this.getCurrentSeconds();

      let minuteTicked = false;
      if (this.seconds === 0) {
        minuteTicked = true;
        this.minutes = this.getCurrentMinutes();
      }

      if (this.minutes === 0 && minuteTicked) {
        this.hours = (this.hours + 1) % 24;
      }
    }, 1000);
  },
};
</script>

<style>
.clock {
  width: 30rem;
  height: 30rem;
  border: 20px solid white;
  border-radius: 50%;
  margin: 50px auto;
  position: relative;
  padding: 2rem;
  box-shadow: 0 0 0 4px rgba(0, 0, 0, 0.1), inset 0 0 0 3px #efefef,
    inset 0 0 10px black, 0 0 10px rgba(0, 0, 0, 0.2);
}

.clock-face {
  position: relative;
  width: 100%;
  height: 100%;
  transform: translateY(-3px);
}
</style>
