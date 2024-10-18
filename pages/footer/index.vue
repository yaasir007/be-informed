<script setup lang="ts">
const email = ref('')

const subscribeNewsletter = () => {
  // Here you would typically send the email to your backend
  console.log('Subscribing email:', email.value)
  // Reset form
  email.value = ''
  // You might want to show a success message to the user here
}
</script>

<template>
  <!-- Footer -->
  <footer class="bg-gray-800 text-white">
    <div class="max-w-7xl mx-auto py-12 px-4 sm:px-6 lg:px-8">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
        <div>
          <h3 class="text-lg font-semibold mb-4">Company Review</h3>
          <p class="text-gray-400">Helping job seekers make informed decisions.</p>
        </div>
        <div>
          <h4 class="text-lg font-semibold mb-4">Quick Links</h4>
          <ul class="space-y-2">
            <li><a href="#" class="text-gray-400 hover:text-white">Home</a></li>
            <li><a href="#" class="text-gray-400 hover:text-white">About Us</a></li>
            <li><a href="#" class="text-gray-400 hover:text-white">Contact</a></li>
            <li><a href="#" class="text-gray-400 hover:text-white">Privacy Policy</a></li>
          </ul>
        </div>
        <div>
          <h4 class="text-lg font-semibold mb-4">Follow Us</h4>
          <div class="flex space-x-4">
            <a href="#" class="text-gray-400 hover:text-white">
              <FacebookIcon class="w-6 h-6" />
            </a>
            <a href="#" class="text-gray-400 hover:text-white">
              <TwitterIcon class="w-6 h-6" />
            </a>
            <a href="#" class="text-gray-400 hover:text-white">
              <LinkedinIcon class="w-6 h-6" />
            </a>
          </div>
        </div>
        <div>
          <h4 class="text-lg font-semibold mb-4">Subscribe</h4>
          <form @submit.prevent="subscribeNewsletter" class="flex">
            <input
              type="email"
              v-model="email"
              placeholder="Enter your email"
              class="flex-grow px-4 py-2 rounded-l-md text-gray-900"
              required
            >
            <button type="submit" class="bg-indigo-600 px-4 py-2 rounded-r-md hover:bg-indigo-700">
              Subscribe
            </button>
          </form>
        </div>
      </div>
      <div class="mt-8 pt-8 border-t border-gray-700 text-center">
        <p class="text-gray-400">&copy; 2023 Company Review. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>

</style>
