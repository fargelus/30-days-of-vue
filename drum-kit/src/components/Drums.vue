<template>
    <div class="drums">
        <div v-for="(sound, index) in sounds">
            <drum-key 
                :title="sound.title"
                :type="sound.type"
                :key="index">
            </drum-key>
        </div>
    </div>
</template>

<script>
import DrumKey from './DrumKey.vue'

export default {
    data() {
        return {
            sounds: [
            {
                title: 'A',
                sound_type: 'clap',
            },
            {
                title: 'S',
                sound_type: 'hihat',
            },
            {
                title: 'D',
                sound_type: 'kick'
            },
            {
                title: 'F',
                sound_type: 'openhat'
            },
            {
                title: 'G',
                sound_type: 'boom'
            },
            {
                title: 'H',
                sound_type: 'ride'
            },
            {
                title: 'J',
                sound_type: 'snare'
            },
            {
                title: 'K',
                sound_type: 'tom'
            },
            {
                title: 'L',
                sound_type: 'tink'
            },
        ]}
    }
};
</script>

<style scoped>
    .drums {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
    }
</style>