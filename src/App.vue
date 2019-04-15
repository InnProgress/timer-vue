<template>
  <div id="main-bg" :class="{ stopped }">
    <div id="app">

      <div id="counter">
        {{ time }}
      </div>

      <actions @timestampChange="setTimestamp" @toggleBackground="(e) => stopped = e" />

    </div>
  </div>
</template>

<script>
import Actions from './components/Actions.vue'

export default {
  data() {
    return {
      time: '00:00:00',
      stopped: true
    }
  },
  methods: {
    setTimestamp(timestamp) {
      var date = new Date(null);
      date.setSeconds(timestamp);
      this.time = date.toISOString().substr(11, 8);

      document.title = this.time;
    }
  },
  components: {
    Actions
  }
}
</script>

<style>
  body {
    margin: 0;
    font-family: 'Poppins', sans-serif;
  }
  #counter {
    text-align: center;
    font-size: 55px;
  }
  #actions {
    text-align: center;
  }
  button {
    background-color: ghostwhite;
    border: 1px solid wheat;
    padding: 12px;
    margin: 0 10px;
    transition-duration: 0.4s;
  }
  button:focus {
    outline: none;
  }
  button:hover {
    background-color: wheat;
    cursor: pointer;
  }
  button i {
    margin-right: 4px;
  }
  #main-bg {
    background-image: linear-gradient(to top, black, #0b6623);
    height: -webkit-fill-available;

    position: relative;
    z-index: 1;
  }
  #main-bg::before {
    position: absolute;
    content: "";
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-image: linear-gradient(to top, black, #B22222);
    z-index: -1;
    transition: opacity 0.5s linear;
    opacity: 0;
  }
  #main-bg.stopped::before {
    opacity: 1;
  }
  #app {
    background-color: ghostwhite;
    width: 340px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 20px;
    box-shadow: 4px 4px 1px wheat;
  }
</style>
