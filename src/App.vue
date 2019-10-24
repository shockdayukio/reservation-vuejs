<template>
  <div id="app">
    <Reservation></Reservation>
    <div>
      <h2>予約</h2>
      <p>10月10日（火）11:00~</p>
    </div>
  </div>
</template>

<script>
import Reservation from './components/Reservation.vue'

export default {
  name: 'app',
  components: {
    Reservation
  }
}
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
