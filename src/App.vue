<template>
  <div id="app">
    <Reservation  v-on:send-reservation="text = $event"></Reservation>
    <p>{{text}}</p>
  </div>
</template>

<script>
import Reservation from './components/Reservation.vue'

export default {
  name: 'app',
  data() {
    return {
      text: "日程未選択です"
    }
  },
  components: {
    Reservation
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
