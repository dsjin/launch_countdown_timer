<template>
  <div class="card-container">
    <div class="before">
      <div class="text">
        {{ number }}
      </div>
    </div>
    <div ref="beforeFlip" class="before-flip">
      <div class="text">
        {{ previousNumber }}
      </div>
    </div>
    <div class="after">
      <div class="text">
        {{ previousNumber }}
      </div>
    </div>
    <div ref="afterFlip" class="after-flip">
      <div class="text">
        {{ number }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'CounterCard',
  props: {
    number: {
      type: String,
      default: '00'
    }
  },
  data () {
    return {
      previousNumber: ''
    }
  },
  watch: {
    number () {
      this.flip()
    }
  },
  mounted () {
    this.previousNumber = this.number
    // requestAnimationFrame(this.flip)
  },
  methods: {
    flip () {
      (this.$refs.beforeFlip as HTMLElement).className = 'before-flip animate';
      (this.$refs.afterFlip as HTMLElement).className = 'after-flip animate'
      setTimeout(() => {
        (this.$refs.beforeFlip as HTMLElement).className = 'before-flip';
        (this.$refs.afterFlip as HTMLElement).className = 'after-flip'
        this.previousNumber = this.number
      }, 950)
    }
  }
})
</script>

<style lang="scss">
  $mobile_width: 600px;
  $desktop_width: 1440px;
  @import '../assets/scss/colors';
  @mixin card-fragment ($background-color) {
    position: absolute;
    height: 50%;
    background-color: $background-color;
  }
  @mixin circle-fragment ($background-color, $length, $position) {
    content: '';
    position: absolute;
    @if $position == 'before-left' {
      left: ($length - ($length / 2)) * -1;
      bottom: ($length - ($length / 2)) * -1;
    }@else if $position == 'before-right' {
      right: ($length - ($length / 2)) * -1;
      bottom: ($length - ($length / 2)) * -1;
    }@else if $position == 'after-left' {
      left: ($length - ($length / 2)) * -1;
      top: ($length - ($length / 2)) * -1;
    }@else if $position == 'after-right' {
      right: ($length - ($length / 2)) * -1;
      top: ($length - ($length / 2)) * -1;
    }
    height: $length;
    width: $length;
    border-radius: 20px;
    background-color: $background-color;
  }
  .card-container {
    border-radius: 10px;
    overflow: hidden;
    position: relative;
    font-size: 5em;
    @media screen and (max-width: $desktop_width) {
      font-size: 5em;
    }
    @media screen and (max-width: $mobile_width) {
      font-size: 3.2em;
    }
    .before, .before-flip {
      @include card-fragment(map-get($colors, 'darkDesaturatedBlue'));
      left: 0;
      right: 0;
      top: 0;
      filter: brightness(85%);
      overflow: hidden;
      &::before {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'before-left')
      }
      &::after {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'before-right')
      }
      .text {
        line-height: calc(min(20vw, 150px));
      }
    }
    .before-flip {
      transform: rotateX(0deg);
      transform-origin: bottom;
      &.animate {
        transition: transform 0.3s ease;
        transform: rotateX(90deg);
      }
    }
    .after, .after-flip {
      @include card-fragment(map-get($colors, 'darkDesaturatedBlue'));
      overflow: hidden;
      left: 0;
      right: 0;
      bottom: 0;
      &::before {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'after-left')
      }
      &::after {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'after-right')
      }
      .text {
        line-height: calc(min(-20vw, -150px));
      }
    }
    .after-flip {
      transform: rotateX(90deg);
      transform-origin: top;
      &.animate {
        transition: transform 1s ease 0.3s;
        transform: rotateX(0deg);
      }
    }
    .text {
      color: map-get($colors, 'softRed');
      text-align: center;
    }
    width: 20vw;
    height: 20vw;
    max-width: 150px;
    max-height: 150px;
    &:not(:last-child) {
      margin-right: 2vw;
    }
  }
</style>
