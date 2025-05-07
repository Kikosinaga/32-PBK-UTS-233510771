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

function removeActivity(index) {
  activities.value.splice(index, 1)
}
</script>

<template>
  <div>
    <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button @click="addActivity">Tambah Kegiatan</button>
    <ul>
      <li v-for="(activity, index) in activities" :key="index">
        {{ activity }}
        <button @click="removeActivity(index)">x</button>
      </li>
    </ul>
  </div>
</template>
