<template>
  <div>
    <button @click="toggleRecord" class="record-btn">{{ icon }}</button>
  </div>
</template>

<script>
export default {
  name: "RecordBtn",
  data() {
    return {
      isRecordStarted: false,
    };
  },

  methods: {
    toggleRecord() {
      this.isRecordStarted = !this.isRecordStarted;
      this.isRecordStarted ? this.$emit("record") : this.$emit("pause");
    },
  },

  computed: {
    icon() {
      return this.isRecordStarted ? "⏸️" : "⏺️";
    },
  },
};
</script>

<style>
.record-btn {
  cursor: pointer;
  background: transparent;
  border: 0;
  font-size: 30px;
  padding: 0;
}
</style>
