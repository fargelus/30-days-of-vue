<template>
  <div class="drums-kit">
    <div class="drums-kit__keys">
      <drum-key
        v-for="sound in sounds"
        @sound="onSound"
        :is-active="!!isCodeActive(sound.code)"
        :key="sound.code"
        :code="sound.code"
        :type="sound.type"
      >
      </drum-key>
    </div>
    <div class="drums-kit__controls">
      <record-btn @record="onRecord" @pause="onPause"></record-btn>
    </div>
  </div>
</template>

<script>
import DrumKey from "./DrumKey.vue";
import RecordBtn from "./RecordBtn.vue";

export default {
  name: "DrumsKit",
  components: { DrumKey, RecordBtn },
  data() {
    return {
      pressedKey: null,
      recordKeys: [],
      recording: false,
      sounds: [
        {
          code: "A",
          type: "clap",
        },
        {
          code: "S",
          type: "hihat",
        },
        {
          code: "D",
          type: "kick",
        },
        {
          code: "F",
          type: "openhat",
        },
        {
          code: "G",
          type: "boom",
        },
        {
          code: "H",
          type: "ride",
        },
        {
          code: "J",
          type: "snare",
        },
        {
          code: "K",
          type: "tom",
        },
        {
          code: "L",
          type: "tink",
        },
      ],
    };
  },

  mounted() {
    addEventListener("keypress", this.setPressedKey);
  },

  methods: {
    setPressedKey(ev) {
      const key = ev.key.toUpperCase();
      this.pressedKey = this.isKeyWatched(key) ? key : null;
      this.checkRecording();
    },

    isKeyWatched(key) {
      return this.sounds.find((sound) => sound.code === key);
    },

    checkRecording() {
      if (this.recording && this.pressedKey) {
        this.recordKeys.push(this.pressedKey);
        this.pressedKey = null;
      }
    },

    isCodeActive(code) {
      return this.pressedKey === code;
    },

    onSound(duration) {
      setTimeout(() => (this.pressedKey = null), duration * 1000);
    },

    onRecord() {
      this.recording = true;
      this.recordKeys = [];
    },

    onPause() {
      this.recording = false;
    },
  },
};
</script>

<style scoped>
.drums-kit {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.drums-kit__keys {
  display: flex;
}

.drums-kit__controls {
  margin-top: 20px;
}
</style>
