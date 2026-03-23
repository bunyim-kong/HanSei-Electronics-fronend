<script setup>
import { ref } from "vue"

const kpis = ref([
{ title:"Total Employees", value:512 },
{ title:"Active Employees", value:486 },
{ title:"New Hires", value:15 },
{ title:"Turnover Rate", value:"4.2%" },
{ title:"Absenteeism", value:"2.5%" }
])

const departments = ref([
{ name:"Engineering", total:95 },
{ name:"Sales", total:120 },
{ name:"HR", total:38 },
{ name:"Marketing", total:60 },
{ name:"Finance", total:45 }
])

const activities = ref([
{ action:"New employee joined", name:"Sarah Kim", time:"2 hours ago"},
{ action:"Promotion", name:"John Lee", time:"Yesterday"},
{ action:"Department Transfer", name:"Emma Chen", time:"2 days ago"}
])

const events = ref([
{ title:"Team Training", date:"Feb 10"},
{ title:"Performance Review", date:"Feb 18"},
{ title:"Company Outing", date:"Feb 25"}
])
</script>

<template>

<div class="min-h-screen bg-white p-10">

<!-- Header -->
<div class="flex justify-between items-center mb-10">
<div>
<h1 class="text-3xl font-bold text-gray-800">HR Analytics Dashboard</h1>
<p class="text-gray-500">Workforce Report</p>
</div>

<button class="bg-blue-600 text-white px-4 py-2 rounded-lg">
Export Report
</button>
</div>


<!-- KPI Section -->
<div class="grid md:grid-cols-2 lg:grid-cols-5 gap-6 mb-10">

<div
v-for="kpi in kpis"
:key="kpi.title"
class="border rounded-xl p-6 hover:shadow-md transition"
>

<p class="text-gray-500 text-sm">{{kpi.title}}</p>
<h2 class="text-3xl font-bold mt-2">{{kpi.value}}</h2>

</div>

</div>


<!-- Charts Section -->
<div class="grid lg:grid-cols-3 gap-8 mb-10">

<div class="border rounded-xl p-6">
<h3 class="font-semibold mb-4">Gender Distribution</h3>

<div class="space-y-4">

<div>
<div class="flex justify-between text-sm">
<span>Male</span>
<span>54%</span>
</div>

<div class="bg-gray-200 h-2 rounded">
<div class="bg-blue-500 h-2 rounded w-[54%]"></div>
</div>

</div>

<div>
<div class="flex justify-between text-sm">
<span>Female</span>
<span>46%</span>
</div>

<div class="bg-gray-200 h-2 rounded">
<div class="bg-purple-500 h-2 rounded w-[46%]"></div>
</div>

</div>

</div>

</div>


<div class="border rounded-xl p-6">
<h3 class="font-semibold mb-4">Employee Growth</h3>

<div class="h-40 flex items-center justify-center text-gray-400">
Chart Area
</div>

</div>


<div class="border rounded-xl p-6">
<h3 class="font-semibold mb-4">Attendance Today</h3>

<div class="space-y-3">

<div class="flex justify-between">
<span>Present</span>
<span>460</span>
</div>

<div class="flex justify-between">
<span>On Leave</span>
<span>22</span>
</div>

<div class="flex justify-between">
<span>Late</span>
<span>14</span>
</div>

</div>

</div>

</div>


<!-- Department + Events -->
<div class="grid lg:grid-cols-2 gap-8 mb-10">

<div class="border rounded-xl p-6">
<h3 class="font-semibold mb-4">Department Headcount</h3>

<div
v-for="dept in departments"
:key="dept.name"
class="mb-4"
>

<div class="flex justify-between text-sm">
<span>{{dept.name}}</span>
<span>{{dept.total}}</span>
</div>

<div class="bg-gray-200 h-2 rounded">

<div
class="bg-blue-500 h-2 rounded"
:style="{width:dept.total/120*100+'%'}"
></div>

</div>

</div>

</div>


<div class="border rounded-xl p-6">
<h3 class="font-semibold mb-4">Upcoming Events</h3>

<div
v-for="event in events"
:key="event.title"
class="flex justify-between py-3 border-b last:border-0"
>

<span>{{event.title}}</span>
<span class="text-gray-400">{{event.date}}</span>

</div>

</div>

</div>


<!-- Activity Feed -->
<div class="border rounded-xl p-6">

<h3 class="font-semibold mb-6">Recent HR Activities</h3>

<div
v-for="activity in activities"
:key="activity.name"
class="flex justify-between border-b py-3 last:border-0"
>

<div>
<p class="font-medium">{{activity.action}}</p>
<p class="text-gray-500 text-sm">{{activity.name}}</p>
</div>

<span class="text-gray-400 text-sm">{{activity.time}}</span>

</div>

</div>

</div>

</template>