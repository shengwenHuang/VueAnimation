<template>
  <div class="container">
    <div>
      <!-- <div class="links">
        <nuxt-link class="button--green" to="/">Back</nuxt-link>
      </div> -->
      <b-card
        title="Planet Animation"
        sub-title="Movement of Sun Earth and Moon"
      >
        <b-card-text>
          <canvas id="canvas" width="300" height="300">Sun Earth Moon </canvas>
        </b-card-text>
      </b-card>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sun: undefined,
      moon: undefined,
      earth: undefined,
    }
  },

  watch: {},
  mounted() {
    this.sun = new Image()
    this.moon = new Image()
    this.earth = new Image()

    this.sun.src = 'https://mdn.mozillademos.org/files/1456/Canvas_sun.png'
    this.moon.src = 'https://mdn.mozillademos.org/files/1443/Canvas_moon.png'
    this.earth.src = 'https://mdn.mozillademos.org/files/1429/Canvas_earth.png'
    this.init()
  },
  methods: {
    init() {
      window.requestAnimationFrame(this.draw)
    },
    draw() {
      const ctx = document.getElementById('canvas').getContext('2d')

      ctx.globalCompositeOperation = 'destination-over'
      ctx.clearRect(0, 0, 300, 300) // clear canvas

      ctx.fillStyle = 'rgba(0, 0, 0, 0.4)'
      ctx.strokeStyle = 'rgba(0, 153, 255, 0.4)'
      ctx.save()
      ctx.translate(150, 150)

      // Earth
      const time = new Date()
      ctx.rotate(
        ((2 * Math.PI) / 60) * time.getSeconds() +
          ((2 * Math.PI) / 60000) * time.getMilliseconds()
      )
      ctx.translate(105, 0)
      ctx.fillRect(0, -12, 40, 24) // Shadow
      ctx.drawImage(this.earth, -12, -12)

      // Moon
      ctx.save()
      ctx.rotate(
        ((2 * Math.PI) / 6) * time.getSeconds() +
          ((2 * Math.PI) / 6000) * time.getMilliseconds()
      )
      ctx.translate(0, 28.5)
      ctx.drawImage(this.moon, -3.5, -3.5)
      ctx.restore()

      ctx.restore()

      ctx.beginPath()
      ctx.arc(150, 150, 105, 0, Math.PI * 2, false) // Earth orbit
      ctx.stroke()

      ctx.drawImage(this.sun, 0, 0, 300, 300)

      window.requestAnimationFrame(this.draw)
    },
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

.links {
  padding-bottom: 15px;
}
</style>
