<template>
  <div class="drum-key" :class="{ 'drum-key--active': isActive }">
    <div class="drum-key__title">{{ code }}</div>
    <div class="drum-key__sound-type">{{ type }}</div>
    <audio ref="sound" :src="`${soundsPath}/${type}.wav`"></audio>
  </div>
</template>

<script type="module">
import { process } from "ipaddr.js";

export default {
  name: "DrumKey",
  props: {
    isActive: Boolean,
    code: String,
    type: String,
  },

  updated() {
    if (this.isActive) {
      this.$refs.sound.play();
      const duration = this.$refs.sound.duration.toFixed(2);
      this.$emit("sound", duration);
    }
  },

  data() {
    return {
      soundsPath: `${process.env.BASE_URL}sounds`,
      styles: {
        color: {
          gold: "#e6a309",
        },
      },
    };
  },
};
</script>

<style scoped>
.drum-key {
  box-sizing: border-box;
  border: 4px solid black;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 80px;
  height: 70px;
  margin-right: 20px;
  border-radius: 4px;
  background: rgba(0, 0, 0, 0.5);
}

.drum-key--active {
  outline: 4px solid v-bind("styles.color.gold");
  border-width: 2px;
}

.drum-key__title {
  color: #fff;
  font-size: 28px;
}

.drum-key__sound-type {
  color: v-bind("styles.color.gold");
  text-transform: uppercase;
  font-size: 10px;
  letter-spacing: 0.1rem;
}
</style>
