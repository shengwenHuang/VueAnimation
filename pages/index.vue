<template>
  <div class="container">
    <div>
      <div class="bubble-wrapper">
        <b-img ref="bubble" center class="bubble-image" src="logo.png" />
      </div>
      <h1 class="title">Vue Animation</h1>
      <div class="links">
        <nuxt-link class="button--green" to="earth/"
          >Planet Animation</nuxt-link
        >
        <nuxt-link class="button--green" to="mouseFollow/"
          >Mouse Following Animation</nuxt-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import { gsap } from 'gsap'
export default {
  data() {
    return {}
  },

  mounted() {
    const { bubble } = this.$refs
    const timeline = gsap.timeline()

    timeline.to(bubble, 0.4, {
      scale: 0.8,
      rotation: 16,
      ease: 'back.out(1.7)',
    })
    timeline.to(bubble, 1.2, {
      scale: 1,
      rotation: '-=16',
      ease: 'elastic.out(2.5, 0.5)',
    })
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.bubble-wrapper {
  position: relative;
}

.bubble {
  position: relative;
  z-index: 3;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgb(12, 105, 17);
  background: #272727;
  border-radius: 50%;
  height: 100px;
  width: 100px;
}

.bubble-pulse {
  position: absolute;
  z-index: 2;
  height: 120px;
  width: 120px;
  top: 50%;
  left: 50%;
  margin-top: -60px;
  margin-left: -60px;
  background: #272727;
  border-radius: 50%;
  opacity: 0;
  transform: scale(0);
}

.bubble-image {
  height: 50%;
}
</style>
