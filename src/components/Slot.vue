<template>
  <div class="slot">
    <h1>レベル：{{level}}</h1>
    <div class="slot-box" v-if="!isLevelChoosing">
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
    <button class="slot-button" @click="resetSlot" v-if="(targetSlot > 3) && !isLevelChoosing">もう一度</button>
    <button class="slot-button" @click="levelChoose" v-if="(targetSlot > 3) && !isLevelChoosing">レベル変更</button>
    <ChangeLevel @level-changed="setLevel" v-if="isLevelChoosing"/>
  </div>
</template>

<script>
import ChangeLevel from './ChangeLevel'

export default {
  name: 'Slot',
  components: {
    ChangeLevel
  },
  data () {
    return {
      targetSlot: 1,
      firstMargin: -20,
      secondMargin: -50,
      thirdMargin: -300,
      level: 3,
      isLevelChoosing: false,
      accurate: {
        1: 5,
        2: 10,
        3: 20,
        4: 35,
        5: 90
      }
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
        vm.firstMargin = (vm.targetSlot <= 1) ? vm.firstMargin - vm.accurate[vm.level] : vm.firstMargin
        vm.secondMargin = (vm.targetSlot <= 2) ? vm.secondMargin - vm.accurate[vm.level] : vm.secondMargin
        vm.thirdMargin = (vm.targetSlot <= 3) ? vm.thirdMargin - vm.accurate[vm.level] : vm.thirdMargin

        if (vm.targetSlot > 3) {
          cancelAnimationFrame(vm.timeCountFrame)
        }
        vm.timeCountFrame = requestAnimationFrame(loop)
      })()
    },
    stopSlot () {
      this.targetSlot++
    },
    resetSlot () {
      this.targetSlot = 1
    },
    levelChoose () {
      this.isLevelChoosing = true
    },
    setLevel (level) {
      this.level = level
      this.isLevelChoosing = false
      this.resetSlot()
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
  padding: 10px;
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
  margin-bottom: 4px;
}
</style>
