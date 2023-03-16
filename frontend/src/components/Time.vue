<script>
import moment from 'moment'
import { startInterval, saveTime, deleteTime } from '../utils/time'

export default {
  props: {
    showSavedTimes: Boolean,
  },
  data() {
    return {
      currentTime: moment().format('HH:mm:ss'),
      savedTimes: [],
    }
  },
  methods: {
    startInterval,
    saveTime,
    deleteTime,
  },
  created: async function () {
    this.startInterval()
    const res = await fetch('http://localhost:5555/times')
    const json = await res.json()
    if (json.length) this.savedTimes = json
  },
}
</script>

<template>
  <div class="greetings">
    <h1 class="purple-neon">{{ currentTime }}</h1>
    <h3 class="white">Натисніть кнопку для збереження в базі даних</h3>
    <button class="btn-wide btn-normal" @click="saveTime">Зберегти час</button>
    <h3 v-if="savedTimes.length && showSavedTimes">
      Раніше збережені часи:
    </h3>
    <div v-if="showSavedTimes" class="deleted-items" v-for="savedTime in savedTimes" :key="savedTime.id">
      <div class="deleted-item">{{ savedTime.time }}</div>
      <button class="btn-sm" @click="() => deleteTime(savedTime.id)">
        Видалити
      </button>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 4rem;
  top: -10px;
}

h3 {
  font-size: 2rem;
}

.btn-sm {
  border-radius: 8px;
  background-color: rgb(255 101 101 / 80%);
  box-shadow: rgb(149 157 165 / 20%) 0px 8px 24px;
  padding: 8px;
  border: 1px solid rgba(192, 98, 98, 0.801);
  cursor: pointer;
  color: black;
}

.deleted-items {
  font-size: 1.7rem;
}

.deleted-item {
  width: 150px;
  display: inline-block;
}

.greetings {
  text-align: center;
}
</style>
