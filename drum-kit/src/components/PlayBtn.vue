<template>
  <div>
    <button :disabled="isDisabled" @click="toggle" class="control-btn">
      {{ icon }}
    </button>
  </div>
</template>

<script>
export default {
  name: "PlayBtn",
  props: {
    isDisabled: Boolean,
  },

  data() {
    return {
      started: false,
    };
  },

  updated() {
    if (this.isDisabled) {
      this.started = false;
    }
  },

  methods: {
    toggle() {
      this.started = !this.started;
      this.started ? this.$emit("play") : this.$emit("pause");
    },
  },

  computed: {
    icon() {
      return this.started ? "⏸️" : "▶️";
    },
  },
};
</script>
