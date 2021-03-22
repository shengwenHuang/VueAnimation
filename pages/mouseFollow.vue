<template>
  <div class="container">
    <head>
      <div class="links">
        <nuxt-link class="button--green" to="/">Back</nuxt-link>
      </div>
      <meta charset="UTF-8" />
      <title>The Eyes</title>
    </head>
    <body>
      <div class="box">
        <div class="eye"></div>
        <div class="eye"></div>
      </div>
    </body>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },

  watch: {},
  mounted() {
    document.querySelector('body').addEventListener('mousemove', this.eyeball)
  },
  methods: {
    eyeball() {
      const eye = document.querySelectorAll('.eye')
      eye.forEach(function (eye) {
        const x = eye.getBoundingClientRect().left + eye.clientWidth / 2
        const y = eye.getBoundingClientRect().top + eye.clientHeight / 2
        const radian = Math.atan2(event.pageX - x, event.pageY - y)
        const rotation = radian * (180 / Math.PI) * -1 + 270
        eye.style.transform = 'rotate(' + rotation + 'deg)'
      })
    },
  },
}
</script>

<style>
/* * {
  margin: 0;
  padding: 0;
}
body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: radial-gradient(#f2761e, #ef4921);
}
.box {
  display: flex;
}
.box .eye {
  position: relative;
  widows: 120px;
  height: 120px;
  display: block;
  background: #fff;
  margin: 0 20px;
  border-radius: 50%;
  box-shadow: 0 5px 45px rgba(0, 0, 0, 0.2), inset 0 0 15px #f2761e,
    inset 0 0 25px #f2761e;
}
.box .eye::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 35px;
  transform: translate(-50%, -50%);
  width: 45px;
  height: 45px;
  border-radius: 50%;
  background: #000;
  border: 10px solid #2196f3;
  box-sizing: border-box;
} */
</style>
