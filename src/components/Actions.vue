<template>
  <div id="actions">
    <button @click="startTimer" v-if="stopped"><i class="fas fa-play"></i> {{ startButtonTxt }}</button>
    <button @click="stopTimer" v-else-if="!stopped"><i class="fas fa-stop"></i> Stop</button>
    <button @click="resetTimer"><i class="fas fa-sync-alt"></i> Reset</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timestamp: 0,
      timer: false,
      stopped: true,
      startButtonTxt: 'Start'
    }
  },
  methods: {
    startTimer() {
      if(!this.timer) {
        this.startButtonTxt = 'Resume';
        this.stopped = false;
        this.timer = setInterval(() => {
          this.timestamp ++;
        }, 1000);
      }
    },
    stopTimer() {
      this.stopped = true;
      clearInterval(this.timer);
      this.timer = false;
    },
    resetTimer() {
      this.timestamp = 0;
      if(!this.stopped) {
        this.stopTimer();
        this.startTimer();
      } else this.startButtonTxt = 'Start';
    }
  },
  watch: {
    timestamp() {
      this.$emit('timestampChange', this.timestamp);
    },
    stopped() {
      this.$emit('toggleBackground', this.stopped);
    }
  }
}
</script>
