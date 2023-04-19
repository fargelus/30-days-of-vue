<template>
    <div class="drums-kit">
        <div v-for="(sound, index) in sounds" :key="index">
            <drum-key 
                :title="sound.title"
                :type="sound.type">
            </drum-key>
        </div>
    </div>
</template>

<script>
import DrumKey from './DrumKey.vue'

export default {
    name: 'DrumsKit',
    components: {DrumKey},
    data() {
        return {
            sounds: [
            {
                title: 'A',
                type: 'clap',
            },
            {
                title: 'S',
                type: 'hihat',
            },
            {
                title: 'D',
                type: 'kick'
            },
            {
                title: 'F',
                type: 'openhat'
            },
            {
                title: 'G',
                type: 'boom'
            },
            {
                title: 'H',
                type: 'ride'
            },
            {
                title: 'J',
                type: 'snare'
            },
            {
                title: 'K',
                type: 'tom'
            },
            {
                title: 'L',
                type: 'tink'
            },
        ]}
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