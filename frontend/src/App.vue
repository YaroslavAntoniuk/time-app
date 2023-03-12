<script setup>
import Time from './components/Time.vue'
</script>

<template>
  <Time :showSavedTimes="true" />
</template>

<style>
@import './assets/base.css';

#app {
  margin: 100px auto;
}

.white {
  color: rgb(79, 80, 79);
}
</style>
