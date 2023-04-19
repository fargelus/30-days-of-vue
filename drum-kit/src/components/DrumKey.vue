<template>
    <div class="drum-key">
        <div class="drum-key__title">{{title}}</div>
        <div class="drum-key__sound-type">{{sound_type}}</div>
        <audio :src="`sounds/${sound_type}.wav`"></audio>
    </div>
</template>

<script type="module">
    export default {
        props: {
            title: String,
            sound_type: String
        }
    }
</script>

<style scoped>
    .drum-key {
      border: 4px solid black;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      width: 80px;
      height: 70px;
      margin-right: 20px;
      border-radius: 4px;
      background: rgba(0, 0, 0, .5);
    }

    .drum-key__title {
      color: #fff;
      font-size: 28px;
    }

    .drum-key__sound-type {
      color: #e6a309;
    }
</style>