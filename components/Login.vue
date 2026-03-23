<template>
  
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white shadow-lg rounded-2xl p-8 w-full max-w-md">

      <!-- Logo -->
      <div class="flex justify-center mb-6">
        <img
          src="https://cdn.discordapp.com/attachments/1480832613760372857/1484379622127829042/Gemini_Generated_Image_f84b5nf84b5nf84b-removebg-preview.png?ex=69be03c0&is=69bcb240&hm=ce672f071b04dc5a41739fd61089ed0c31fbd910090cc7d4584bd72679d0b91d&"
          alt="Company Logo"
          class="h-20 w-50 object-contain"
        />
      </div>

      <h2 class="text-2xl font-bold text-gray-800 text-center mb-6">Welcome Back</h2>
      <p class="text-gray-500 text-center mb-6">Please login to your account</p>

      <form @submit.prevent="login">
        <div class="mb-4">
          <label class="block text-gray-700 font-medium mb-2">Email</label>
          <input
            v-model="email"
            type="email"
            placeholder="Enter your email"
            class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400"
            required
          />
        </div>

        <div class="mb-4">
          <label class="block text-gray-700 font-medium mb-2">Password</label>
          <input
            v-model="password"
            type="password"
            placeholder="Enter your password"
            class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400"
            required
          />
        </div>

        <div class="flex items-center justify-between mb-6">
          <label class="flex items-center text-gray-700">
            <input type="checkbox" v-model="rememberMe" class="mr-2" />
            Remember me
          </label>
          <NuxtLink to="/pw" class="text-blue-500 hover:underline text-sm">Forgot password?</NuxtLink>
        </div>

        <button
          type="submit"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg transition duration-200"
        >
          Login
        </button>
      </form>

      <p class="text-gray-500 text-center mt-6 text-sm">
        Don't have an account?
        <NuxtLink to="/signup" class="text-blue-500 hover:underline">Sign Up</NuxtLink>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')
const rememberMe = ref(false)

const login = () => {
  console.log('Login:', email.value, password.value, rememberMe.value)
  router.push('/dashboard') // Navigate to dashboard
}
</script>