<template>
  <div>
    <img class="icon" src="../assets/carrot.jpg">
    <h1 class="message">{{ msg }}</h1>
    <button class="button-start" v-on:click="$emit('click-start-button')">スタート</button>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  data () {
    return {
      msg: '俺を揃えてくれよ！'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.message {
  font-size: 1.5rem;
}
.icon {
  width: 100%;
}
.button-start {
  color: #fff;
  font-size: 1rem;
  padding: 10px;
  font-weight: bold;
  background: #60BCF5;
  border: none;
  outline: none;
}
.button-start:active{
  background: #b8daf0;
}
</style>
