<template>
  <div class="change-level">
    <h1>レベルを選択</h1>
    <button class="change-level-button" @click="$emit('level-changed', 1)">1</button>
    <button class="change-level-button" @click="$emit('level-changed', 2)">2</button>
    <button class="change-level-button" @click="$emit('level-changed', 3)">3</button>
    <button class="change-level-button" @click="$emit('level-changed', 4)">4</button>
    <button class="change-level-button" @click="$emit('level-changed', 5)">5</button>
  </div>
</template>

<script>
export default {
  name: 'ChangeLevel'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.change-level-button {
  color: #fff;
  font-size: 1rem;
  padding: 20px;
  font-weight: bold;
  background: #60BCF5;
  border: none;
  outline: none;
}
.change-level-button:active{
  background: #b8daf0;
}
</style>
