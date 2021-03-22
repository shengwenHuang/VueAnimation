<template>
  <div class="container">
    <canvas
      id="canvas"
      width="600"
      height="300"
      style="border: 1px solid black"
    ></canvas>
  </div>
</template>

<script>
export default {
  data() {
    return {
      running: false,
      ball: {
        x: 0,
        y: 0,
        vx: 5,
        vy: 1,
        radius: 25,
        color: 'black',
      },
    }
  },

  watch: {
    // ball: {
    //   deep: true,
    //   handler() {
    //     if (!this.running) {
    //       this.drawBall()
    //     }
    //   },
    // },
  },
  mounted() {
    this.canvas = document.getElementById('canvas')
    this.ctx = this.canvas.getContext('2d')
    const vm = this

    this.canvas.addEventListener('mousemove', function (e) {
      if (!vm.running) {
        vm.clear()
        vm.ball.x = e.offsetX
        vm.ball.y = e.offsetY
        vm.drawBall()
      }
    })

    this.canvas.addEventListener('click', function (e) {
      // vm.raf = window.requestAnimationFrame(vm.draw)
      if (!vm.running) {
        vm.raf = window.requestAnimationFrame(vm.draw)
        vm.running = true
      }
    })

    this.canvas.addEventListener('mouseout', function (e) {
      window.cancelAnimationFrame(vm.raf)
      vm.running = false
    })

    this.drawBall()
  },
  methods: {
    clear() {
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
    },
    draw() {
      this.clear()
      this.drawBall()
      this.ball.x += this.ball.vx
      this.ball.y += this.ball.vy

      if (
        this.ball.y + this.ball.vy > this.canvas.height ||
        this.ball.y + this.ball.vy < 0
      ) {
        this.ball.vy = -this.ball.vy
      }
      if (
        this.ball.x + this.ball.vx > this.canvas.width ||
        this.ball.x + this.ball.vx < 0
      ) {
        this.ball.vx = -this.ball.vx
      }

      this.raf = window.requestAnimationFrame(this.draw)
    },
    drawBall() {
      this.ctx.beginPath()
      // console.log('ddd', this.ball.x, this.ball.y)
      this.ctx.arc(
        this.ball.x,
        this.ball.y,
        this.ball.radius,
        0,
        Math.PI * 2,
        true
      )
      this.ctx.closePath()
      this.ctx.fillStyle = this.ball.color
      this.ctx.fill()
      // console.log('drawb')
    },
  },
}
</script>

<style></style>
