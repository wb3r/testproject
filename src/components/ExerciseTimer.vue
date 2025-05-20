<script setup lang="ts">
import { ref } from 'vue'

type Mode = 'idle' | 'exercise' | 'setBreak' | 'break' | 'finished'

const totalExercises = ref(5)
const setsPerExercise = ref(3)
const exerciseDuration = ref(30)
const setBreakDuration = ref(5)
const breakDuration = ref(60)

const timeLeft = ref(exerciseDuration.value)
const mode = ref<Mode>('idle')
const currentExercise = ref(1)
const currentSet = ref(1)
let interval: ReturnType<typeof setInterval> | null = null

function start() {
  if (interval) clearInterval(interval)
  if (mode.value === 'idle' || mode.value === 'finished') {
    currentExercise.value = 1
    currentSet.value = 1
    mode.value = 'exercise'
    timeLeft.value = exerciseDuration.value
  }
  interval = setInterval(tick, 1000)
}

function pause() {
  if (interval) {
    clearInterval(interval)
    interval = null
  }
}

function reset() {
  pause()
  mode.value = 'idle'
  timeLeft.value = exerciseDuration.value
  currentExercise.value = 1
  currentSet.value = 1
}

function tick() {
  if (timeLeft.value > 0) {
    timeLeft.value--
  } else {
    advance()
  }
}

function advance() {
  if (mode.value === 'exercise') {
    if (currentSet.value < setsPerExercise.value) {
      mode.value = 'setBreak'
      timeLeft.value = setBreakDuration.value
    } else {
      mode.value = 'break'
      timeLeft.value = breakDuration.value
    }
  } else if (mode.value === 'setBreak') {
    currentSet.value++
    mode.value = 'exercise'
    timeLeft.value = exerciseDuration.value
  } else if (mode.value === 'break') {
    if (currentExercise.value < totalExercises.value) {
      currentExercise.value++
      currentSet.value = 1
      mode.value = 'exercise'
      timeLeft.value = exerciseDuration.value
    } else {
      mode.value = 'finished'
      pause()
    }
  }
}
</script>

<template>
  <div class="space-y-4 text-center">
    <div class="text-4xl font-bold">
      <span v-if="mode !== 'finished'">{{ timeLeft }}</span>
      <span v-else>Done!</span>
    </div>
    <div class="flex justify-center gap-4">
      <div>Exercise {{ currentExercise }} / {{ totalExercises }}</div>
      <div>Set {{ currentSet }} / {{ setsPerExercise }}</div>
    </div>
    <div class="join">
      <button class="btn join-item" @click="start">Start</button>
      <button class="btn join-item" @click="pause">Pause</button>
      <button class="btn join-item" @click="reset">Reset</button>
    </div>
  </div>
</template>
