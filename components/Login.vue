<template>
  <div class="min-h-screen grid grid-cols-1 lg:grid-cols-2">

     <!-- Left Side (Branding) -->
    <div class="hidden lg:flex flex-col justify-center bg-indigo-600 text-white p-16">
      <div class="max-w-md">
        <h1 class="text-4xl font-bold mb-6">
          HR Management System
        </h1>

        <p class="text-lg opacity-90 mb-10">
          Manage employees, attendance, and HR operations in one powerful system.
        </p>

        <div class="space-y-4 text-sm">
          <div class="flex items-center gap-3">
            <Users class="w-5 h-5"/>
            <span>Employee Management</span>
          </div>

          <div class="flex items-center gap-3">
            <Clock class="w-5 h-5"/>
            <span>Attendance Tracking</span>
          </div>

          <div class="flex items-center gap-3">
            <BarChart3 class="w-5 h-5"/>
            <span>HR Analytics Dashboard</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Right Side -->
    <div class="flex items-center justify-center bg-gray-100 p-6">

      <div class="w-full max-w-md bg-white p-8 rounded-2xl shadow-xl">

        <h2 class="text-2xl font-bold text-gray-800 mb-6">
          Sign in
        </h2>

        <!-- Error Message -->
        <div v-if="errorMessage"
             class="mb-4 bg-red-100 text-red-600 text-sm p-3 rounded-lg">
          {{ errorMessage }}
        </div>

        <!-- Email -->
        <div class="mb-4">
          <label class="text-sm text-gray-600">Email</label>
          <input
            v-model="form.email"
            type="email"
            placeholder="Enter email"
            class="w-full border rounded-lg px-3 py-2 mt-1 outline-none focus:ring-2 focus:ring-indigo-500"
          />
        </div>

        <!-- Password -->
        <div class="mb-5">
          <label class="text-sm text-gray-600">Password</label>
          <input
            v-model="form.password"
            type="password"
            placeholder="Enter password"
            class="w-full border rounded-lg px-3 py-2 mt-1 outline-none focus:ring-2 focus:ring-indigo-500"
          />
        </div>

        <!-- Login Button -->
        <button
          @click="handleLogin"
          :disabled="loading"
          class="w-full bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-lg font-medium transition disabled:opacity-50"
        >
          {{ loading ? "Logging in..." : "Login" }}
        </button>

        <!-- Register -->
        <p class="text-sm text-gray-500 text-center mt-6">
          Don't have an account?
          <NuxtLink to="/signup"
            class="text-indigo-600 font-medium hover:underline ml-1">
            Register
          </NuxtLink>
        </p>

      </div>

    </div>

  </div>
</template>

<script setup>
import { ref } from "vue"
import { useRouter } from "vue-router"
import { Mail, Lock, Users, Clock, BarChart3, User } from "lucide-vue-next"


const router = useRouter()

const form = ref({
  email: "",
  password: ""
})

const loading = ref(false)
const errorMessage = ref("")

const handleLogin = async () => {
  errorMessage.value = ""
  loading.value = true

  try {
    // 🔹 Call your backend API
    const { data, error } = await useFetch("http://localhost:5000/api/login", {
      method: "POST",
      body: form.value
    })

    if (error.value) {
      throw new Error("Invalid email or password")
    }

    // Example: if backend returns token
    if (data.value?.token) {
      localStorage.setItem("token", data.value.token)
      router.push("/dashboard")
    } else {
      throw new Error("Login failed")
    }

  } catch (err) {
    errorMessage.value = "Invalid email or password. Please try again."
  } finally {
    loading.value = false
  }
}
</script>