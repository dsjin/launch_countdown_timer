<template>
  <div
    id="main"
  >
    <div
      id="content-container"
    >
      <h1
        id="header1"
      >
        {{ header1 }}
      </h1>
      <counter-card />
    </div>
    <div
      id="hills"
    >
      <social-link />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CounterCard from './components/CounterCard.vue'
import SocialLink from './components/SocialLink.vue'

interface Data {
  header1: string
}

export default defineComponent({
  name: 'App',
  components: { SocialLink, CounterCard },
  data () : Data {
    return {
      header1: 'WE\'RE LAUNCHING SOON'
    }
  }
})
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Red+Hat+Text:wght@700&display=swap');
  @import './assets/scss/colors';
  $mobile_width: 375px;
  $desktop_width: 1440px;
  body {
    font-family: 'Red Hat Text', sans-serif;
    margin: 0;
  }
  #main {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    font-size: 14px;
    background-color: map-get($colors, "veryDarkestBlue");
    background-image: url('./assets/bg-stars.svg');
    height: 100vh;
    @media screen and (max-width: $mobile_width) {
      max-width: $mobile_width;
    }
    @media screen and (max-width: $desktop_width) {
      max-width: $desktop_width;
    }
    #content-container {
      #header1 {
        color: map-get($colors, "white");
        margin: 0;
        letter-spacing: 0.2em
      }
    }
    #hills {
      position: absolute;
      bottom: 0;
      background-image: url('./assets/pattern-hills.svg');
      background-size: cover;
      background-position: center center;
      background-repeat: no-repeat;
      height: 197px;
      width: 100%;
    }
  }
</style>
