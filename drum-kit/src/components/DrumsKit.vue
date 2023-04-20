<template>
    <div class="drums-kit">
        <drum-key v-for="sound in sounds"
            :key="sound.code"
            :code="sound.code"
            :type="sound.type">
        </drum-key>
        <div>{{this.pressedKey}}</div>
    </div>
</template>

<script>
import DrumKey from './DrumKey.vue'

export default {
    name: 'DrumsKit',
    components: {DrumKey},
    data() {
        return {
            pressedKey: null,
            sounds: [
            {
                code: 'A',
                type: 'clap',
            },
            {
                code: 'S',
                type: 'hihat',
            },
            {
                code: 'D',
                type: 'kick'
            },
            {
                code: 'F',
                type: 'openhat'
            },
            {
                code: 'G',
                type: 'boom'
            },
            {
                code: 'H',
                type: 'ride'
            },
            {
                code: 'J',
                type: 'snare'
            },
            {
                code: 'K',
                type: 'tom'
            },
            {
                code: 'L',
                type: 'tink'
            },
        ]}
    },
    mounted() {
        addEventListener('keypress', this.setPressedKey);
    },
    methods: {
        setPressedKey(ev) {
            const key = ev.key.toUpperCase();
            this.pressedKey = this.isKeyWatched(key) ? key : null;
        },

        isKeyWatched(key) {
            return this.sounds.find(sound => sound.code === key);
        }
    }
};
</script>

<style scoped>
    .drums-kit {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
    }
</style>