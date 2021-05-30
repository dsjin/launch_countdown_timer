<template>
  <div
    id="social-container"
  >
    <div
      :key="index"
      v-for="(link, index) in links"
      class="social-item"
    >
      <img :src="link.img" alt="social icon">
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

interface LinkInfo {
  img: string
  path: string
}

interface Data {
  links: LinkInfo[]
}

export default defineComponent({
  name: 'SocialLink',
  data () : Data {
    return {
      links: [
        {
          img: require('@/assets/icon-facebook.svg'),
          path: ''
        },
        {
          img: require('@/assets/icon-pinterest.svg'),
          path: ''
        },
        {
          img: require('@/assets/icon-instagram.svg'),
          path: ''
        }
      ]
    }
  }
})
</script>

<style lang="scss">
  #social-container {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .social-item{
      &:not(:last-child) {
        margin-right: 2em;
      }
      cursor: pointer;
      &:hover {
        filter: invert(55%) sepia(15%) saturate(4599%) hue-rotate(309deg) brightness(99%) contrast(99%);
      }
    }
  }
</style>
