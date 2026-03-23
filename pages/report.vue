<template>
  <div class="min-h-screen bg-sky-50 p-6">

    <!-- Header -->
    <h1 class="text-3xl font-bold text-sky-800 mb-6">📊 Display Reports</h1>

    <!-- Tabs -->
     
    <div class="flex gap-4 mb-6">
      <button
        v-for="tab in tabs"
        :key="tab"
        @click="activeTab = tab"
        :class="[
          'px-4 py-2 rounded-lg font-medium',
          activeTab === tab ? 'bg-sky-600 text-white' : 'bg-white shadow'
        ]"
      >
        {{ tab }}
      </button>
    </div>

    <!-- ================= ATTENDANCE HISTORY ================= -->
    <div v-if="activeTab === 'Attendance History'" class="bg-white rounded-xl shadow overflow-x-auto">
      <table class="min-w-full text-left">
        <thead class="bg-sky-100 text-sky-800">
          <tr>
            <th class="px-4 py-2">Employee</th>
            <th class="px-4 py-2">Check In</th>
            <th class="px-4 py-2">Check Out</th>
            <th class="px-4 py-2">Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="emp in attendance" :key="emp.id" class="border-b">
            <td class="px-4 py-2">{{ emp.name }}</td>
            <td class="px-4 py-2">{{ emp.checkIn  }}</td>
            <td class="px-4 py-2">{{ emp.checkOut }}</td>
            <td class="px-4 py-2">
              <span :class="emp.status === 'present' ? 'text-green-600' : 'text-red-500'">
                {{ emp.status }}
              </span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- ================= LEAVE HISTORY ================= -->
    <div v-if="activeTab === 'Leave History'" class="bg-white rounded-xl shadow overflow-x-auto">
      <table class="min-w-full text-left">
        <thead class="bg-red-100 text-red-700">
          <tr>
            <th class="px-4 py-2">Employee</th>
            <th class="px-4 py-2">Leave Type</th>
            <th class="px-4 py-2">Start Date</th>
            <th class="px-4 py-2">End Date</th>
            <th class="px-4 py-2">Reason</th>
            <th class="px-4 py-2">Status</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="leave in leaves" :key="leave.id" class="border-b">
            <td class="px-4 py-2">{{ leave.name }}</td>
            <td class="px-4 py-2">{{ leave.type }}</td>
            <td class="px-4 py-2">{{ leave.start }}</td>
            <td class="px-4 py-2">{{ leave.end }}</td>
            <td class="px-4 py-2">{{ leave.reason }}</td>
            <td class="px-4 py-2">
              <span
                :class="{
                  'text-green-600': leave.status === 'approved',
                  'text-yellow-500': leave.status === 'pending',
                  'text-red-500': leave.status === 'rejected'
                }"
              >
                {{ leave.status }}
              </span>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- ================= SALARY OVERVIEW ================= -->
    <div v-if="activeTab === 'Salary Overview'" class="bg-white rounded-xl shadow overflow-x-auto">
      <table class="min-w-full text-left">
        <thead class="bg-blue-100 text-blue-800">
          <tr>
            <th class="px-4 py-2">Employee</th>
            <th class="px-4 py-2">Base Salary</th>
            <th class="px-4 py-2">OT Salary</th>
            <th class="px-4 py-2">Total Salary</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="emp in salary" :key="emp.id" class="border-b">
            <td class="px-4 py-2">{{ emp.name }}</td>
            <td class="px-4 py-2">${{ emp.basicSalary }}</td>
            <td class="px-4 py-2">${{ calculateOT(emp).toFixed(2) }}</td>
            <td class="px-4 py-2 font-bold text-green-600">
              ${{ calculateTotal(emp).toFixed(2) }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const tabs = ['Attendance History', 'Leave History', 'Salary Overview']
const activeTab = ref('Attendance History')
// Attendance Data
const attendance = ref([
  { id: 1, name: 'John Doe', checkIn: '09:00', checkOut: '17:00', status: 'present' },
  { id: 2, name: 'Jane Smith', checkIn: null, checkOut: null, status: 'absent' },
])

// Leave Data (NEW 🔥)
const leaves = ref([
  { id: 1, name: 'John Doe', type: 'Sick Leave', start: '2026-03-01', end: '2026-03-02', reason: 'Fever', status: 'approved' },
  { id: 2, name: 'Jane Smith', type: 'Annual Leave', start: '2026-03-05', end: '2026-03-07', reason: 'Trip', status: 'pending' },
])

// Salary Data
const salary = ref([
  { id: 1, name: 'John Doe', basicSalary: 500, hoursWorked: 160, otHours: 10, otRate: 15 },
  { id: 2, name: 'Jane Smith', basicSalary: 450, hoursWorked: 160, otHours: 5, otRate: 12 },
])

const calculateOT = (emp) => emp.otHours * emp.otRate
const calculateTotal = (emp) => (emp.basicSalary / 160) * emp.hoursWorked + calculateOT(emp)
</script>