<script setup>
import { computed, ref } from 'vue'
const score = ref('')
const valid = computed(() => score.value !== '' && Number.isFinite(Number(score.value)) && Number(score.value) >= 0 && Number(score.value) <= 100)
const grade = computed(() => {
  if (!valid.value) return ''
  const n = Number(score.value)
  if (n >= 80) return 'A'
  if (n >= 75) return 'B+'
  if (n >= 70) return 'B'
  if (n >= 65) return 'C+'
  if (n >= 60) return 'C'
  if (n >= 55) return 'D+'
  if (n >= 50) return 'D'
  return 'F'
})
</script>
<template>
  <h1 class="h3 mb-3">โปรแกรมคำนวณเกรด</h1>
  <div class="card shadow-sm" style="max-width:540px"><div class="card-body">
    <label for="score" class="form-label">กรอกคะแนน (0–100)</label>
    <input id="score" v-model="score" type="number" min="0" max="100" step="any" class="form-control" placeholder="เช่น 82" />
    <div v-if="score !== '' && !valid" class="text-danger small mt-2">โปรดกรอกคะแนนตั้งแต่ 0 ถึง 100</div>
    <div v-if="valid" class="alert alert-success mt-3 mb-0">คะแนน {{ score }} ได้เกรด <strong>{{ grade }}</strong></div>
  </div></div>
  <p class="text-secondary small mt-3">เกณฑ์คะแนน: A 80–100, B+ 75–79, B 70–74, C+ 65–69, C 60–64, D+ 55–59, D 50–54, F ต่ำกว่า 50</p>
</template>
