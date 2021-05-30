<template>
  <div class="card-container">
    <div class="before" />
    <div class="after" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'CounterCard'
})
</script>

<style lang="scss">
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
    border-radius: 15px;
    overflow: hidden;
    position: relative;
    .before {
      @include card-fragment(map-get($colors, 'darkDesaturatedBlue'));
      left: 0;
      right: 0;
      top: 0;
      filter: brightness(85%);
      &::before {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'before-left')
      }
      &::after {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'before-right')
      }
    }
    .after {
      @include card-fragment(map-get($colors, 'darkDesaturatedBlue'));
      left: 0;
      right: 0;
      bottom: 0;
      &::before {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'after-left')
      }
      &::after {
        @include circle-fragment(map-get($colors, 'veryDarkestBlue'), 20px, 'after-right')
      }
    }
    width: 200px;
    height: 200px;
  }
</style>
