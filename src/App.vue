<template>
  <div
    id="main"
  >
    <h1
      id="header1"
    >
      {{ header1 }}
    </h1>
    <div
      id="content-container"
    >
      <div
        id="timer-counter-container"
      >
        <counter-card :number="time.days" />
        <counter-card :number="time.hours" />
        <counter-card :number="time.minutes" />
        <counter-card :number="time.seconds" />
      </div>
      <div id="label-timer-counter">
        <p>
          DAYS
        </p>
        <p>
          HOURS
        </p>
        <p>
          MINUTES
        </p>
        <p>
          SECONDS
        </p>
      </div>
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
  totalSeconds: number
  time: {
    days: string
    hours: string
    minutes: string
    seconds: string
  }
  timer: number | undefined
}

export default defineComponent({
  name: 'App',
  components: { SocialLink, CounterCard },
  data () : Data {
    return {
      header1: 'WE\'RE LAUNCHING SOON',
      totalSeconds: 129600,
      time: {
        days: '00',
        hours: '00',
        minutes: '00',
        seconds: '00'
      },
      timer: undefined
    }
  },
  mounted () {
    if (!this.timer) {
      this.timer = setInterval(() => {
        this.time = {
          ...this.convertSectoDay(this.totalSeconds)
        }
        this.totalSeconds -= 1
      }, 1000)
    }
  },
  methods: {
    convertSectoDay (n: number) {
      const days = parseInt(`${n / (24 * 3600)}`)
      n = n % (24 * 3600)
      const hours = parseInt(`${n / 3600}`)
      n %= 3600
      const minutes = parseInt(`${n / 60}`)
      n %= 60
      const seconds = n
      return {
        days: this.formatePrefixZero(days),
        hours: this.formatePrefixZero(hours),
        minutes: this.formatePrefixZero(minutes),
        seconds: this.formatePrefixZero(seconds)
      }
    },
    formatePrefixZero (n: number) : string {
      if (n <= 9) {
        return `0${n}`
      }
      return `${n}`
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
    flex-direction: column;
    #header1 {
      color: map-get($colors, "white");
      margin: 0;
      letter-spacing: 0.2em;
      text-align: center;
      position: absolute;
      top: 8em;
      @media screen and (max-width: $desktop_width) {
        font-size: 2em;
      }
      @media screen and (max-width: $mobile_width) {
        top: 7em;
        font-size: 1.8em;
      }
    }
    #content-container {
      #timer-counter-container {
        padding: 20px;
        justify-content: space-between;
        display: flex;
      }
      #label-timer-counter {
        color: map-get($colors, "graylishBlue");
        justify-content: space-between;
        display: flex;
        padding-left: 20px;
        padding-right: 20px;
        padding-bottom: 20px;
        text-align: center;
        p {
          width: 20vw;
          max-width: 150px;
          letter-spacing: 0.2em;
          font-size: 0.8em;
          &:not(:last-child) {
            margin-right: 2vw;
          }
        }
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
