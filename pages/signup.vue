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

    <!-- Right Side (Signup Form) -->
    <div class="flex items-center justify-center bg-gray-100 p-6">
      <div class="w-full max-w-md bg-white p-8 rounded-2xl shadow-xl">

        <h2 class="text-2xl font-bold text-gray-800 mb-2">
          Create Account
        </h2>

        <p class="text-gray-500 mb-6">
          Register to access the HR dashboard
        </p>

        <!-- Full Name -->
        <div class="mb-4">
          <label class="text-sm text-gray-600">Full Name</label>
          <div class="flex items-center border rounded-lg px-3 mt-1">
            <User class="w-5 h-5 text-gray-400 mr-2"/>
            <input
              type="text"
              placeholder="Enter your full name"
              class="w-full py-2 outline-none"
            />
          </div>
        </div>

        <!-- Email -->
        <div class="mb-4">
          <label class="text-sm text-gray-600">Email</label>
          <div class="flex items-center border rounded-lg px-3 mt-1">
            <Mail class="w-5 h-5 text-gray-400 mr-2"/>
            <input
              type="email"
              placeholder="Enter your email"
              class="w-full py-2 outline-none"
            />
          </div>
        </div>

        <!-- Password -->
        <div class="mb-5">
          <label class="text-sm text-gray-600">Password</label>
          <div class="flex items-center border rounded-lg px-3 mt-1">
            <Lock class="w-5 h-5 text-gray-400 mr-2"/>
            <input
              type="password"
              placeholder="Create a password"
              class="w-full py-2 outline-none"
            />
          </div>
        </div>

        <!-- Signup Link -->
        <NuxtLink
          to="/dashboard"
          class="block text-center w-full bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-lg font-medium transition"
        >
          Register
        </NuxtLink>

        <!-- Back to login -->
        <p class="text-sm text-gray-500 text-center mt-6">
          Already have an account?
          <NuxtLink
            to="/login"
            class="text-indigo-600 font-medium hover:underline ml-1"
          >
            Login
          </NuxtLink>
        </p>

        

      </div>
    </div>

  </div>
</template>

<script setup>
import { Mail, Lock, Users, Clock, BarChart3, User } from "lucide-vue-next"
</script>