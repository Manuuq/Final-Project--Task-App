<template>
  <div class="clock">
    {{ time }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      time: new Date().toLocaleTimeString()
    };
  },
  mounted() {
    this.interval = setInterval(() => {
      this.time = new Date().toLocaleTimeString();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.interval);
  }
};
</script>

<style scoped>
.clock {
  font-size: 3rem;
  text-align: center;
  margin-top: 50px;
}
</style>