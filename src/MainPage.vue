<script setup>
import { ref } from 'vue'
import bot from "./assets/bot.png"
const url = ref('')
const sendMessage = async () => {
  try {
    const response = await fetch('https://your-backend-url/api/submit-url', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ url: url.value }), // Send the url in the request body
    });

    if (!response.ok) {
      throw new Error('Failed to send the URL');
    }

    const data = await response.json();
    console.log('Success:', data);
  } catch (error) {
    console.error('Error:', error);
  }
};


</script>

<template>
<div class="bg-gradient-to-r from-gray-500 to-blue-900 justify-center w-full h-screen flex flex-col md:flex-row">
    
    <!-- Left Side: Logo and Welcome Message -->
    <div class="flex flex-col justify-center items-center w-full lg:w-1/2 p-6 lg:pl-16">
      <img :src="bot" class="h-32 w-auto mb-4 md:h-40" /> <!-- Adjusted size for mobile and desktop -->
      <h1 class="text-3xl md:text-5xl font-bold text-white mb-2 md:mb-4">Welcome to Bop!</h1> <!-- Smaller on mobile -->
      <p class="text-lg md:text-xl font-light text-white text-center md:text-left">Please enter the URL to get started.</p>
    </div>

    <!-- Right Side: URL Input -->
    <div class="flex flex-col justify-center items-center w-full lg:w-1/2 p-6 lg:pr-16">
      <div class="w-full max-w-xl">
        <form @submit.prevent="sendMessage">
          <input
            v-model="url"
            type="text"
            placeholder="Enter the URL"
            class="w-full p-4 md:p-5 bg-gray-700 text-white outline-none rounded-lg shadow-lg focus:ring-2 focus:ring-blue-500 transition-all duration-200"
          />
        </form>
      </div>
    </div>

  </div>
</template>

<style scoped>

</style>

