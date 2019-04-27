<template>
  <div id="app">
    <ColorPicker :color="color" />
    <Canvas :pixels="pixels" />
  </div>
</template>

<script>
import Canvas from './components/Canvas'
import ColorPicker from './components/ColorPicker'

const defaultColor = 'white'

export default {
  name: 'App',
  data: function() {
    return {
      color: defaultColor,
      pixels: Array(30 * 30)
        .fill()
        .map(() => defaultColor)
    }
  },
  components: {
    Canvas,
    ColorPicker
  },
  mounted() {
    this.$root.$on('updatecolor', color => {
      this.color = color
    })
    this.$root.$on('clickedpixel', index => {
      this.pixels.splice(index, 1, this.color)
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
body {
  box-sizing: border-box;
  margin:0;
  padding:0;
}

h1, h2, h3, h4, h5, h6, p {
  margin: 0;
}

*, *:before, *:after {
  box-sizing: inherit;
}
</style>
