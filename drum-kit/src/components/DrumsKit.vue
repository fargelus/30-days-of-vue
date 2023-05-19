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
      <play-btn
        @play="onPlay"
        :is-disabled="isPlayBtnDisabled()"
        :playing="playing"
      ></play-btn>
      <record-btn @record="onRecord" @pause="onPause"></record-btn>
    </div>
  </div>
</template>

<script>
import DrumKey from "./DrumKey.vue";
import PlayBtn from "./PlayBtn.vue";
import RecordBtn from "./RecordBtn.vue";

export default {
  name: "DrumsKit",
  components: { DrumKey, PlayBtn, RecordBtn },
  data() {
    return {
      pressedKey: null,
      recordKeys: [],
      recording: false,
      playing: false,
      playingGenerator: null,
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
      this.pressedKey = this.isKeyEqlCode(key) ? key : null;
      this.checkRecording();
    },

    isKeyEqlCode(key) {
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
      setTimeout(() => (this.pressedKey = this.nextSound()), duration * 1000);
    },

    nextSound() {
      return this.playing ? this.playingGenerator.next().value : null;
    },

    onRecord() {
      this.recording = true;
      this.recordKeys = [];
    },

    onPause() {
      this.recording = false;
    },

    playingIterator: function* () {
      for (const sound of this.recordKeys) {
        yield sound;
      }
      this.playing = false;
    },

    onPlay() {
      this.playing = true;
      this.playingGenerator = this.playingIterator();
      this.pressedKey = this.playingGenerator.next().value;
    },

    isPlayBtnDisabled() {
      return this.recordKeys.length == 0 || this.recording;
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

.drums-kit__keys,
.drums-kit__controls {
  display: flex;
}

.drums-kit__controls {
  margin-top: 20px;
}

.drums-kit__controls > div {
  margin-right: 15px;
}
</style>
