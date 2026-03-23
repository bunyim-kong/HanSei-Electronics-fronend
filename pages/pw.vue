<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="bg-white shadow-lg rounded-2xl p-8 w-full max-w-md">

      <div class="flex justify-center mb-6">
        <img
          src="https://cdn.discordapp.com/attachments/1480832613760372857/1484379622127829042/Gemini_Generated_Image_f84b5nf84b5nf84b-removebg-preview.png?ex=69be03c0&is=69bcb240&hm=ce672f071b04dc5a41739fd61089ed0c31fbd910090cc7d4584bd72679d0b91d&"
          alt="Company Logo"
          class="h-20 w-50 object-contain"
        />
      </div>

      <h2 class="text-2xl font-bold text-gray-800 text-center mb-6">Forgot Password</h2>
      <p class="text-gray-500 text-center mb-6">Enter your email to reset your password</p>

      <form @submit.prevent="resetPassword">
        <div class="mb-4">
          <label class="block text-gray-700 font-medium mb-2">Email</label>
          <input type="email" v-model="email" placeholder="Enter your email"
            class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-400" required />
        </div>

        <button type="submit"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 rounded-lg transition duration-200">
          Send Reset Link
        </button>
      </form>

      <p class="text-gray-500 text-center mt-6 text-sm">
        Remembered your password?
        <NuxtLink to="/" class="text-blue-500 hover:underline">Login</NuxtLink>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')

const resetPassword = () => {
  console.log('Reset password email:', email.value)
  alert(`Password reset link sent to ${email.value}`)
}
</script>