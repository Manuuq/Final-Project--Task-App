<template>
    <div class="clock">
      {{ time }}
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        time: ''
      }
    },
    mounted() {
      setInterval(() => {
        this.time = new Date().toLocaleTimeString();
      }, 1000);
    }
  }
  </script>
  
  <style>
  .clock {
    font-size: 2rem;
    text-align: center;
    padding: 2rem;
  }
  </style>
  