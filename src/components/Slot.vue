<template>
  <div class="slot">
    <h1>Slot</h1>
    <div class="slot-box">
      <div class="slot-box-column slot-box-column_up">
        <img
          class="slot-image"
          style="margin-top:45px"
          :style="{marginLeft : firstMargin + 'px' }"
          src="../assets/slot-character.jpg"
          alt
        >
      </div>
      <div class="slot-box-column slot-box-column_middle">
        <img
          style="margin-top:-78px"
          :style="{marginLeft : secondMargin + 'px' }"
          src="../assets/slot-character.jpg"
          alt
        >
      </div>
      <div class="slot-box-column slot-box-column_down">
        <img
          style="margin-top:-203px"
          :style="{marginLeft : thirdMargin + 'px' }"
          src="../assets/slot-character.jpg"
          alt
        >
      </div>
    </div>
    <button class="slot-button" @click="stopSlot" v-if="targetSlot <= 3">Stop</button>
    <button class="slot-button" @click="resetSlot" v-if="targetSlot > 3">もう一度あそぶ</button>
  </div>
</template>

<script>
export default {
  name: 'Slot',
  data () {
    return {
      targetSlot: 1,
      firstMargin: -20,
      secondMargin: -50,
      thirdMargin: -300
    }
  },
  mounted () {
    this.startSlot()
  },
  methods: {
    startSlot () {
      const vm = this
      this.firstMargin = Math.round(Math.random() * 1000 * -1)
      this.secondMargin = Math.round(Math.random() * 1000 * -1)
      this.thirdMargin = Math.round(Math.random() * 1000 * -1);

      (function loop () {
        if (vm.firstMargin < -1000) {
          vm.firstMargin = 0
        }
        if (vm.secondMargin < -1000) {
          vm.secondMargin = 0
        }
        if (vm.thirdMargin < -1000) {
          vm.thirdMargin = 0
        }
        vm.firstMargin = (vm.targetSlot <= 1) ? vm.firstMargin - 5 : vm.firstMargin
        vm.secondMargin = (vm.targetSlot <= 2) ? vm.secondMargin - 5 : vm.secondMargin
        vm.thirdMargin = (vm.targetSlot <= 3) ? vm.thirdMargin - 5 : vm.thirdMargin

        if (vm.targetSlot > 3) {
          cancelAnimationFrame(vm.timeCountFrame)
        }
        vm.timeCountFrame = requestAnimationFrame(loop)
      })()
    },
    stopSlot () {
      this.targetSlot++
      console.log(this.targetSlot)
    },
    resetSlot () {
      this.targetSlot = 1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 0;
}

.slot {
  width: 100%;
  height: 100%;
}

.slot-box {
  width: 100%;
  height: 70%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.slot-box-column {
  width: 220px;
  height: 120px;
  border: solid 2px #000;
  background: #fff;
  overflow: hidden;
}

.slot-button {
  display: inline-block;
  font-size: 1.1rem;
  padding: 15px;
  text-decoration: none;
  background: #d69953;
  color: #FFF;
  border-bottom: solid 4px #b38551;
  border-radius: 3px;
  outline: none;
}

.slot-button:active {
    transform: translateY(4px);
    border-bottom: none;
}
</style>
