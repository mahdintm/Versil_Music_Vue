<template>
  <div id="VG_musicVue">
    <IntroVue v-if="IntroVue.isActive"></IntroVue>
  </div>
</template>

<script>
import IntroVue from './components/Intro.vue'
export default {
  name: 'App',
  components: {
    IntroVue
  },
  data() {
    return {
      IntroVue: { isActive: true },
      WebViewEvents: {
        musicVue: {
          mountedAndReady: "WEBclient:MusicVue:mountedAndReady",
        },
        IntroVue: {
          load: "ClientWEB:IntroMusic:Load",
          unLoad: "ClientWEB:IntroMusic:unLoad",
        },
      }
    }
  },
  created() {
    if ('alt' in window) {
      alt.on(this.WebViewEvents.IntroVue.load, () => {
        this.IntroVue.isActive = true;
      })
      alt.on(this.WebViewEvents.IntroVue.unLoad, () => {
        this.IntroVue.isActive = false;
      })
    }
  },
  mounted() {
    if ("alt" in window) {
      alt.emit(this.WebViewEvents.musicVue.mountedAndReady);
    }
  }
}
</script>

<style>
* {
  display: none;
}

body {
  display: none;
}
</style>
