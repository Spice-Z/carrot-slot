<template>
  <div id="app">
    <Welcome @click-start-button="moveNextStep()" v-if="step == 1"/>
    <Slot v-if="step==2" />
  </div>
</template>

<script>
import Slot from './components/Slot'
import Welcome from './components/Welcome'

export default {
  name: 'App',
  components: {
    Slot,
    Welcome
  },
  data () {
    return {
      step: 1
    }
  },
  mounted () {
    this.track()
  },
  methods: {
    track () {
      this.$ga.page('/')
    },
    moveNextStep () {
      this.step++
    }
  }
}
</script>

<style>
html{
  font-size: 125%;
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
}
body {
  width: 100%;
  height: 100%;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  height: 100%;
}
</style>
