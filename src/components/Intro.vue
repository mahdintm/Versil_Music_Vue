<template>
    <div>
        <audio autoplay id="audio-player" loop>
            <source src=".././assets/musics/intro1.ogg" type="audio/ogg" />
        </audio>
    </div>
</template>

<script>
export default {
    name: 'IntroVue',
    data() {
        return {
            WebViewEvents: {
                introMusic: {
                    changeVolume: "ClientWEB:introMusic:changeVolume",
                },
            },
        }
    },
    unmounted() {
        if ("alt" in window) {
            alt.off(this.WebViewEvents.introMusic.changeVolume, this.ChangeVolume);
        }
    },
    mounted() {
        if ("alt" in window) {
            alt.on(this.WebViewEvents.introMusic.changeVolume, this.ChangeVolume);
        }
        document.getElementById('audio-player').volume = 0.3;
    },
    methods: {
        ChangeVolume(VolumeLevel) {
            document.getElementById('audio-player').volume = VolumeLevel;
        }
    }
}
</script>

<style>
#audio-player {
    display: none;
}
</style>