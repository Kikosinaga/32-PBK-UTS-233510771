
<script setup>
import { ref, computed } from 'vue'

const activities = ref([
  { text: "olahraga", done: false },
  { text: "Makan", done: false },
  { text: "Tidur", done: false }
])
const newActivity = ref('')
const filter = ref('all') // all, done, notdone

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ text: newActivity.value.trim(), done: false })
    newActivity.value = ''
  }
}

function removeActivity(activity) {
  const index = activities.value.indexOf(activity)
  if (index > -1) {
    activities.value.splice(index, 1)
  }
}

// Removed toggleDone function as it is unused

const filteredActivities = computed(() => {
  if (filter.value === 'done') {
    return activities.value.filter(a => a.done)
  } else if (filter.value === 'notdone') {
    return activities.value.filter(a => !a.done)
  } else {
    return activities.value
  }
})
</script>

<template>
  <div>
    <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button @click="addActivity">Tambah Kegiatan</button>
    <div>
      <button @click="filter = 'all'">Semua</button>
      <button @click="filter = 'done'">Selesai</button>
      <button @click="filter = 'notdone'">Belum Selesai</button>
    </div>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <input type="checkbox" v-model="activity.done" />
        <span :style="{ textDecoration: activity.done ? 'line-through' : 'none' }">{{ activity.text }}</span>
        <button @click="removeActivity(activity)">x</button>
      </li>
    </ul>
  </div>
</template>
