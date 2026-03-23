<template>
  <div class="flex h-screen bg-gray-100">
    <!-- Sidebar -->
    <aside class="w-64 bg-white shadow-md p-4">
      <h2 class="text-xl font-bold mb-6">Attendance</h2>
      <nav class="space-y-3">
        <a href="#" class="block text-blue-600 font-semibold">Dashboard</a>
        <a href="#" class="block text-gray-600">My Attendance</a>
        <a href="#" class="block text-gray-600">Team Attendance</a>
        <a href="#" class="block text-gray-600">Calendar</a>
        <a href="#" class="block text-gray-600">Leave Requests</a>
      </nav>
    </aside>

    <!-- Main -->
    <div class="flex-1 p-6 overflow-y-auto">
      <!-- Header -->
      <div class="flex justify-between items-center mb-6">
        <h1 class="text-2xl font-bold">Welcome back, {{ user.name }}</h1>
        <input
          type="text"
          placeholder="Search..."
          class="border px-3 py-2 rounded-lg"
        />
      </div>

      <!-- Stats -->
      <div class="grid grid-cols-4 gap-4 mb-6">
        <div class="bg-white p-4 rounded-xl shadow">
          <p class="text-gray-500">Present</p>
          <h2 class="text-2xl font-bold">{{ stats.present }}</h2>
        </div>
        <div class="bg-white p-4 rounded-xl shadow">
          <p class="text-gray-500">Leave</p>
          <h2 class="text-2xl font-bold">{{ stats.leave }}</h2>
        </div>
        <div class="bg-white p-4 rounded-xl shadow">
          <p class="text-gray-500">Late</p>
          <h2 class="text-2xl font-bold">{{ stats.late }}</h2>
        </div>
        <div class="bg-white p-4 rounded-xl shadow">
          <p class="text-gray-500">Absent</p>
          <h2 class="text-2xl font-bold">{{ stats.absent }}</h2>
        </div>
      </div>

      <!-- Attendance Table -->
      <div class="bg-white rounded-xl shadow p-4">
        <div class="flex justify-between mb-4">
          <h2 class="text-lg font-semibold">Today's Attendance</h2>
          <button class="text-blue-600">View All</button>
        </div>

        <table class="w-full text-left">
          <thead>
            <tr class="text-gray-500 border-b">
              <th class="py-2">Employee</th>
              <th>Check In</th>
              <th>Check Out</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="emp in employees" :key="emp.id" class="border-b">
              <td class="py-3">{{ emp.name }}</td>
              <td>{{ emp.checkIn || '-' }}</td>
              <td>{{ emp.checkOut || '-' }}</td>
              <td>
                <span
                  :class="statusClass(emp.status)"
                  class="px-2 py-1 rounded text-sm"
                >
                  {{ emp.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Check In / Out Section -->
      <div class="mt-6 bg-white p-6 rounded-xl shadow flex justify-between items-center">
        <div>
          <h2 class="text-lg font-semibold">Your Attendance</h2>
          <p class="text-gray-500">{{ currentStatus }}</p>
        </div>
        <div class="space-x-3">
          <button
            @click="checkIn"
            class="bg-green-500 text-white px-4 py-2 rounded-lg"
          >
            Check In
          </button>
          <button
            @click="checkOut"
            class="bg-red-500 text-white px-4 py-2 rounded-lg"
          >
            Check Out
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const user = ref({ name: 'Alex' })

const stats = ref({
  present: 247,
  leave: 23,
  late: 8,
  absent: 5
})

const employees = ref([
  { id: 1, name: 'Sarah', checkIn: '09:02 AM', checkOut: null, status: 'Present' },
  { id: 2, name: 'Mike', checkIn: '08:45 AM', checkOut: '06:15 PM', status: 'Present' },
  { id: 3, name: 'Emma', checkIn: '09:15 AM', checkOut: null, status: 'Late' },
  { id: 4, name: 'John', checkIn: '08:30 AM', checkOut: '05:45 PM', status: 'Present' }
])

const currentStatus = ref('Not Checked In')

const checkIn = () => {
  currentStatus.value = 'Checked In'
}

const checkOut = () => {
  currentStatus.value = 'Checked Out'
}

const statusClass = (status) => {
  switch (status) {
    case 'Present': return 'bg-green-100 text-green-600'
    case 'Late': return 'bg-yellow-100 text-yellow-600'
    case 'Absent': return 'bg-red-100 text-red-600'
    default: return 'bg-gray-100 text-gray-600'
  }
}
</script>

<style>
body {
  font-family: Inter, sans-serif;
}
</style>