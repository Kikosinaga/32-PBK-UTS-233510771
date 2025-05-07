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
  <div class="background">
    <div class="todo-container">
      <h1>Todo List</h1>
      <div class="input-group">
        <input type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
        <button @click="addActivity">Tambah Kegiatan</button>
      </div>
      <div class="filter-buttons">
        <button :class="{ active: filter === 'all' }" @click="filter = 'all'">Semua</button>
        <button :class="{ active: filter === 'done' }" @click="filter = 'done'">Selesai</button>
        <button :class="{ active: filter === 'notdone' }" @click="filter = 'notdone'">Belum Selesai</button>
      </div>
      <ul class="activity-list">
        <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
          <input type="checkbox" v-model="activity.done" />
          <span :style="{ textDecoration: activity.done ? 'line-through' : 'none' }">{{ activity.text }}</span>
          <button class="delete-btn" @click="removeActivity(activity)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.background {
  background-image: url('https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1350&q=80');
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  min-height: 100vh;
  padding: 40px 0;
  display: flex;
  justify-content: center;
  align-items: flex-start;
}

.todo-container {
  max-width: 400px;
  padding: 20px;
  background-color: rgba(240, 248, 255, 0.708); /* aliceblue with transparency */
  border-radius: 8px;
  font-family: Arial, sans-serif;
  box-shadow: 0 4px 8px rgba(0,0,0,0.5);
}

h1 {
  text-align: center;
  color: #2f4f4f; 
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex-grow: 1;
  padding: 8px 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

button {
  padding: 8px 16px;
  background-color: #4682b4; 
  border: none;
  border-radius: 4px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #315f86; /* darker steel blue */
}

.filter-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

.filter-buttons button {
  background-color: #b0c4de; /* light steel blue */
  color: #333;
  font-weight: normal;
}

.filter-buttons button.active {
  background-color: #315f86; /* darker steel blue */
  color: white;
  font-weight: bold;
}

.activity-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.activity-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 12px;
  background-color: white;
  border-radius: 4px;
  margin-bottom: 10px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.activity-item span {
  flex-grow: 1;
  font-size: 16px;
  color: #333;
}

.delete-btn {
  background-color: transparent;
  border: none;
  color: #315f86; /* darker steel blue */
  font-weight: bold;
  cursor: pointer;
  font-size: 16px;
  line-height: 1;
  padding: 0;
}

.delete-btn:hover {
  color: #4682b4; /* steel blue */
}
</style>
