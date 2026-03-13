<template>
  <div class="min-h-screen bg-blue-50 p-8">

    <!-- Header -->
    <h1 class="text-3xl font-bold text-blue-800 mb-6">Salary & OT Management</h1>

    <!-- Employee Table -->
    <div class="bg-white shadow rounded-xl overflow-x-auto">
      <table class="min-w-full text-left">
        <thead class="bg-blue-100 text-blue-800">
          <tr>
            <th class="px-4 py-2">Employee</th>
            <th class="px-4 py-2">Basic Salary ($)</th>
            <th class="px-4 py-2">Hours Worked</th>
            <th class="px-4 py-2">OT Hours</th>
            <th class="px-4 py-2">OT Rate ($/h)</th>
            <th class="px-4 py-2">OT Salary ($)</th>
            <th class="px-4 py-2">Total Salary ($)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="emp in employees" :key="emp.id" class="border-b hover:bg-blue-50">
            <td class="px-4 py-2 flex items-center gap-2">
              <img :src="emp.avatar" class="w-8 h-8 rounded-full" />
              {{ emp.name }}
            </td>
            <td class="px-4 py-2">
              <input type="number" v-model.number="emp.basicSalary" class="border rounded px-2 py-1 w-24" />
            </td>
            <td class="px-4 py-2">
              <input type="number" v-model.number="emp.hoursWorked" class="border rounded px-2 py-1 w-20" />
            </td>
            <td class="px-4 py-2">
              <input type="number" v-model.number="emp.otHours" class="border rounded px-2 py-1 w-20" />
            </td>
            <td class="px-4 py-2">
              <input type="number" v-model.number="emp.otRate" class="border rounded px-2 py-1 w-20" />
            </td>
            <td class="px-4 py-2 font-medium">{{ calculateOT(emp).toFixed(2) }}</td>
            <td class="px-4 py-2 font-bold">{{ calculateTotal(emp).toFixed(2) }}</td>
          </tr>

          <!-- Totals Row -->
          <tr class="bg-blue-100 font-semibold text-blue-800">
            <td class="px-4 py-2">Total</td>
            <td class="px-4 py-2">{{ totalBaseSalary.toFixed(2) }}</td>
            <td class="px-4 py-2">{{ totalHours }}</td>
            <td class="px-4 py-2">{{ totalOTHours }}</td>
            <td class="px-4 py-2">{{ totalOTSalary.toFixed(2) }}</td>
            <td class="px-4 py-2"></td>
            <td class="px-4 py-2">{{ totalPayout.toFixed(2) }}</td>
          </tr>
        </tbody>
      </table>

      <!-- Salary Summary at Bottom -->
      <div class="bg-blue-500 text-white rounded-b-xl p-6 mt-4 flex flex-col md:flex-row justify-between items-center">
        <p>Total Base Salary: <span class="font-bold">${{ totalBaseSalary.toFixed(2) }}</span></p>
        <p>Total OT Salary: <span class="font-bold">${{ totalOTSalary.toFixed(2) }}</span></p>
        <p class="mt-2 md:mt-0 text-lg font-bold">Total Payout: ${{ totalPayout.toFixed(2) }}</p>
      </div>
    </div>

  </div>
</template>

<script setup>
import { reactive, computed } from 'vue'

// Sample dynamic employee data
const employees = reactive([
  { id: 1, name: 'Alice', avatar: 'https://i.pravatar.cc/40?img=1', basicSalary: 500, hoursWorked: 160, otHours: 10, otRate: 15 },
  { id: 2, name: 'Bob', avatar: 'https://i.pravatar.cc/40?img=2', basicSalary: 450, hoursWorked: 160, otHours: 5, otRate: 12 },
  { id: 3, name: 'Charlie', avatar: 'https://i.pravatar.cc/40?img=3', basicSalary: 600, hoursWorked: 160, otHours: 8, otRate: 20 },
])

// Functions for calculation
const calculateOT = (emp) => emp.otHours * emp.otRate
const calculateTotal = (emp) => {
  const hourlyRate = emp.basicSalary / 160
  return hourlyRate * emp.hoursWorked + calculateOT(emp)
}

// Computed properties
const totalBaseSalary = computed(() => employees.reduce((sum, e) => sum + e.basicSalary, 0))
const totalOTSalary = computed(() => employees.reduce((sum, e) => sum + calculateOT(e), 0))
const totalPayout = computed(() => employees.reduce((sum, e) => sum + calculateTotal(e), 0))
const totalHours = computed(() => employees.reduce((sum, e) => sum + e.hoursWorked, 0))
const totalOTHours = computed(() => employees.reduce((sum, e) => sum + e.otHours, 0))
</script>