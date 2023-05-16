<template>
  <div>
    <button @click="toggleRecord" class="control-btn">{{ icon }}</button>
  </div>
</template>

<script>
export default {
  name: "RecordBtn",
  data() {
    return {
      started: false,
    };
  },

  methods: {
    toggleRecord() {
      this.started = !this.started;
      this.started ? this.$emit("record") : this.$emit("pause");
    },
  },

  computed: {
    icon() {
      return this.started ? "⏸️" : "⏺️";
    },
  },
};
</script>
