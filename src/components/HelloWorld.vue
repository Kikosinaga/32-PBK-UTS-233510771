<script setup>
import { ref } from 'vue'

const activities = ref(["olahraga","Makan","Tidur"])
const newActivity = ref('')

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push(newActivity.value.trim())
    newActivity.value = ''
  }
}
</script>

<template>
  <div>
    <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button @click="addActivity">Tambah Kegiatan</button>
    <ul>
      <li v-for="(activity, index) in activities" :key="index">{{ activity }}</li>
    </ul>
  </div>
</template>
