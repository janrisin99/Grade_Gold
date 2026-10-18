<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
const apiUrl = 'https://api.gold-api.com/price/XAU'
const gold = ref(null)
const loading = ref(false)
const error = ref('')
let intervalId
const formattedPrice = computed(() => gold.value ? new Intl.NumberFormat('en-US', {minimumFractionDigits:2,maximumFractionDigits:2}).format(gold.value.price) : '')
const formattedTime = computed(() => {
  if (!gold.value?.updatedAt) return 'API ไม่ได้ระบุเวลา'
  const d = new Date(gold.value.updatedAt)
  return Number.isNaN(d.getTime()) ? gold.value.updatedAt : d.toLocaleString('th-TH', {dateStyle:'medium',timeStyle:'medium'})
})
async function fetchGold() {
  loading.value = true
  error.value = ''
  try {
    const response = await fetch(apiUrl, {cache:'no-store'})
    if (!response.ok) throw new Error(`API ตอบกลับ HTTP ${response.status}`)
    const data = await response.json()
    if (typeof data.price !== 'number' || !Number.isFinite(data.price)) throw new Error('ไม่พบราคาทองคำที่ถูกต้อง')
    gold.value = data
  } catch (err) {
    error.value = `โหลดข้อมูลไม่สำเร็จ: ${err.message}`
  } finally { loading.value = false }
}
onMounted(() => {fetchGold(); intervalId = setInterval(fetchGold, 60000)})
onUnmounted(() => clearInterval(intervalId))
</script>
<template>
  <h1 class="h3">ราคาทองคำผ่าน API</h1>
  <p class="text-secondary">ข้อมูลทองคำ Spot (XAU) หน่วย USD ต่อทรอยออนซ์ ไม่ใช่ราคาทองแท่งไทย</p>
  <div class="card shadow-sm" style="max-width:720px"><div class="card-body p-4">
    <div class="d-flex justify-content-between align-items-center gap-3 flex-wrap"><h2 class="h5 mb-0">Gold Spot (XAU/USD)</h2><button type="button" class="btn btn-outline-dark btn-sm" :disabled="loading" @click="fetchGold">{{ loading ? 'กำลังโหลด...' : 'รีเฟรชราคา' }}</button></div>
    <div v-if="gold" class="mt-3"><div class="display-5 fw-bold">${{ formattedPrice }}</div><div class="text-secondary">USD / troy oz</div><p class="small mt-3 mb-0">เวลาอัปเดตจาก API: {{ formattedTime }}</p></div>
    <div v-if="loading && !gold" class="alert alert-info mt-3 mb-0">กำลังดึงข้อมูลจาก API...</div>
    <div v-if="error" class="alert alert-danger mt-3 mb-0" role="alert">{{ error }}</div>
  </div></div>
  <p class="small mt-3">ที่มา: <a :href="apiUrl" target="_blank" rel="noopener noreferrer">{{ apiUrl }}</a> (อัปเดตอัตโนมัติทุก 60 วินาที)</p>
</template>
