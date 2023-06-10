<template>
  <select @change="setTimeWithinZone" class="timezone-picker">
    <option :key="index" v-for="(tmz, index) in timezones" :value="tmz">
      {{ tmz }}
    </option>
  </select>
</template>

<script>
export default {
  name: "TimezonePicker",
  data() {
    return {
      timezones: [],
      timeInZone: null,
      formatOptions: {
        hour: "numeric",
        minute: "numeric",
      },
      formatLocale: "en-GB",
      localDate: new Date(),
    };
  },

  created() {
    const currentZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
    this.timezones.push(currentZone);

    const allZones = Intl.supportedValuesOf("timeZone");
    for (let tz of allZones) {
      if (tz === currentZone) {
        continue;
      }

      this.timezones.push(tz);
    }
  },

  methods: {
    setTimeWithinZone(ev) {
      const pickedZone = ev.target.value;
      this.formatOptions["timeZone"] = pickedZone;
      this.timeInZone = new Intl.DateTimeFormat(
        this.formatLocale,
        this.formatOptions
      ).format(this.localDate);
    },
  },
};
</script>

<style>
.timezone-picker {
  position: absolute;
  right: 5%;
  top: 20px;
}
</style>
