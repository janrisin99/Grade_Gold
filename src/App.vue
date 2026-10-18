<script setup>
import { ref } from 'vue'
import GradeCalculator from './views/GradeCalculator.vue'
import GoldPrice from './views/GoldPrice.vue'
const currentPage = ref('gold')
</script>
<template>
  <header class="bg-dark text-white py-3 mb-4"><div class="container d-flex flex-wrap align-items-center justify-content-between gap-2">
    <strong>Vue.js API Assignment</strong>
    <nav class="d-flex gap-2"><button type="button" class="btn" :class="currentPage === 'gold' ? 'btn-warning' : 'btn-outline-light'" @click="currentPage = 'gold'">ราคาทองคำ API</button><button type="button" class="btn" :class="currentPage === 'grade' ? 'btn-warning' : 'btn-outline-light'" @click="currentPage = 'grade'">คำนวณเกรด</button></nav>
  </div></header>
  <main class="container pb-5"><GoldPrice v-if="currentPage === 'gold'"/><GradeCalculator v-else/></main>
</template>
