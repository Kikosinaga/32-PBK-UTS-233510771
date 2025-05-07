<script setup>
import { ref } from 'vue'

const activities = ref([
  { text: "olahraga", done: false },
  { text: "Makan", done: false },
  { text: "Tidur", done: false }
])
const newActivity = ref('')

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ text: newActivity.value.trim(), done: false })
    newActivity.value = ''
  }
}

function removeActivity(index) {
  activities.value.splice(index, 1)
}

function toggleDone(activity) {
  activity.done = !activity.done
}
</script>

<template>
  <div>
    <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button @click="addActivity">Tambah Kegiatan</button>
    <ul>
      <li v-for="(activity, index) in activities" :key="index">
        <input type="checkbox" v-model="activity.done" />
        <span :style="{ textDecoration: activity.done ? 'line-through' : 'none' }">{{ activity.text }}</span>
        <button @click="removeActivity(index)">x</button>
      </li>
    </ul>
  </div>
</template>
