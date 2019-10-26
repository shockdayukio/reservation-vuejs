<template>
  <div id="app">
    <Reservation  v-on:send-reservation="date = $event"></Reservation>
    <p>{{date}}</p>
  </div>
</template>

<script>
import Reservation from './components/Reservation.vue'

export default {
  name: 'app',
  data() {
    return {
      date: null
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
