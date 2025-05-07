<script setup>
import { ref } from 'vue'

const activities = ref(["olahraga","Makan","Tidur"])
const newActivity = ref('')
</script>

<template>
  <div>
    <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button>Tambah Kegiatan</button>
    <ul>
      <li v-for="(activity, index) in activities" :key="index">{{ activity }}</li>
    </ul>
  </div>
</template>
