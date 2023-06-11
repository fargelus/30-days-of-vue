<template>
  <div class="timezone-picker">
    <input
      type="text"
      v-model="userTimezoneSearch"
      @input="filterZones"
      placeholder="Search zone"
    />
    <select @change="setTimeWithinZone">
      <option
        :key="index"
        v-for="(tmz, index) in filteredTimeZones"
        :value="tmz"
      >
        {{ tmz }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "TimezonePicker",
  data() {
    return {
      userTimezoneSearch: "",
      timezones: [],
      filteredTimeZones: [],
      timeInZone: null,
      formatOptions: {
        hour: "numeric",
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

    this.filteredTimeZones = this.timezones;
  },

  methods: {
    setTimeWithinZone(ev) {
      const pickedZone = ev.target.value;
      this.formatOptions["timeZone"] = pickedZone;
      this.hourInZone = new Intl.DateTimeFormat(
        this.formatLocale,
        this.formatOptions
      ).format(this.localDate);
      this.$emit("hours-changed", this.hourInZone);
    },

    filterZones() {
      if (this.userTimezoneSearch == "") {
        this.filteredTimeZones = this.timezones;
        return;
      }

      this.filteredTimeZones = this.timezones.filter((zone) =>
        zone.includes(this.userTimezoneSearch)
      );
    },
  },
};
</script>

<style>
.timezone-picker {
  display: flex;
  flex-direction: column;
  position: absolute;
  right: 5%;
  top: 20px;
}
</style>
