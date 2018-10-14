<template>
  <div id="app">
    <v-app>
      <h3 class="white--text mt-5">Age Calculator</h3>
      <date-picker></date-picker>
    </v-app>
  </div>
</template>

<script>
  import DatePicker from './components/DatePicker.vue';

  export default {
    name: 'app',
    components: {
      DatePicker
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
    background: rgb(0, 0, 0);
  }
  h3 {
    font-size: 30px;
  }
</style>
