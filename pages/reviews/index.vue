<script setup lang="ts">
import { ref } from 'vue'
import { StarIcon } from 'lucide-vue-next'

const newReview = ref({
  rating: '',
  text: ''
})

const reviews = ref([
  {
    id: 1,
    userName: 'John Doe',
    avatar: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOuxrvcNMfGLh73uKP1QqYpKoCB0JLXiBMvA&s',
    rating: 4,
    text: 'Great company to work for! The work-life balance is excellent, and there are many opportunities for growth.'
  },
  {
    id: 2,
    userName: 'Jane Smith',
    avatar: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOuxrvcNMfGLh73uKP1QqYpKoCB0JLXiBMvA&s',
    rating: 3,
    text: 'Decent workplace with good benefits, but the management could be more transparent about company decisions.'
  }
])

const submitReview = () => {
  const review = {
    id: reviews.value.length + 1,
    userName: 'Anonymous User', // In a real app, this would be the logged-in user's name
    avatar: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOuxrvcNMfGLh73uKP1QqYpKoCB0JLXiBMvA&s',
    rating: parseInt(newReview.value.rating),
    text: newReview.value.text
  }

  reviews.value.unshift(review)

  // Reset form
  newReview.value = {
    rating: '',
    text: ''
  }
}
</script>

<template>
  <nav class="bg-white shadow">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex">
          <div class="flex-shrink-0 flex items-center">
            <span class="ml-2 text-xl font-bold text-[#4F45E4]">BeInformed</span>
          </div>
        </div>
        <div class="hidden sm:ml-6 sm:flex sm:space-x-8">
          <a href="/" class="border-indigo-500 text-gray-900 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">
            Home
          </a>
          <a href="./reviews.vue" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">
            Companies
          </a>
          <NuxtLink to="./reviews" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Reviews</NuxtLink>
          <a href="#" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">
            About
          </a>
        </div>
        <div class="hidden sm:ml-6 sm:flex sm:items-center">
          <button class="bg-indigo-600 text-white px-4 py-2 rounded-md text-sm font-medium hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            Sign In
          </button>
        </div>
        <div class="-mr-2 flex items-center sm:hidden">
          <button @click="toggleMobileMenu" type="button" class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500" aria-controls="mobile-menu" :aria-expanded="mobileMenuOpen">
            <span class="sr-only">Open main menu</span>
            <MenuIcon v-if="!mobileMenuOpen" class="block h-6 w-6" />
            <XIcon v-else class="block h-6 w-6" />
          </button>
        </div>
      </div>
    </div>

    <!-- Mobile menu, show/hide based on menu state. -->
    <div v-show="mobileMenuOpen" class="sm:hidden" id="mobile-menu">
      <div class="pt-2 pb-3 space-y-1">
        <a href="#" class="bg-indigo-50 border-indigo-500 text-indigo-700 block pl-3 pr-4 py-2 border-l-4 text-base font-medium">Home</a>
        <a href="#" class="border-transparent text-gray-500 hover:bg-gray-50 hover:border-gray-300 hover:text-gray-700 block pl-3 pr-4 py-2 border-l-4 text-base font-medium">Companies</a>
        <a href="#" class="border-transparent text-gray-500 hover:bg-gray-50 hover:border-gray-300 hover:text-gray-700 block pl-3 pr-4 py-2 border-l-4 text-base font-medium">Reviews</a>
        <a href="#" class="border-transparent text-gray-500 hover:bg-gray-50 hover:border-gray-300 hover:text-gray-700 block pl-3 pr-4 py-2 border-l-4 text-base font-medium">About</a>
      </div>
      <div class="pt-4 pb-3 border-t border-gray-200">
        <div class="mt-3 space-y-1">
          <button class="w-full text-left block px-4 py-2 text-base font-medium text-gray-500 hover:text-gray-800 hover:bg-gray-100">
            Sign In
          </button>
        </div>
      </div>
    </div>
  </nav>

  <div class="min-h-screen bg-gray-100 py-8 px-4 sm:px-6 lg:px-8">
    <div class="max-w-4xl mx-auto">
      <h1 class="text-3xl font-bold text-center text-gray-900 mb-8">Company Reviews</h1>

      <!-- Review Form -->
      <div class="bg-white shadow-md rounded-lg p-6 mb-8">
        <h2 class="text-2xl font-semibold mb-4">Leave a Review</h2>
        <form @submit.prevent="submitReview">
          <div class="mb-4">
            <label for="rating" class="block text-sm font-medium text-gray-700 mb-1">Rating</label>
            <select
              id="rating"
              v-model="newReview.rating"
              class="w-full border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500"
              required
            >
              <option value="" disabled>Select a rating</option>
              <option v-for="i in 5" :key="i" :value="i">{{ i }} Star{{ i > 1 ? 's' : '' }}</option>
            </select>
          </div>
          <div class="mb-4">
            <label for="review" class="block text-sm font-medium text-gray-700 mb-1">Review</label>
            <textarea
              id="review"
              v-model="newReview.text"
              rows="4"
              class="w-full border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500"
              required
            ></textarea>
          </div>
          <button
            type="submit"
            class="w-full bg-indigo-600 text-white py-2 px-4 rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            Submit Review
          </button>
        </form>
      </div>

      <!-- Existing Reviews -->
      <div class="bg-white shadow-md rounded-lg p-6">
        <h2 class="text-2xl font-semibold mb-4">Recent Reviews</h2>
        <div v-if="reviews.length === 0" class="text-gray-500 text-center">
          No reviews yet. Be the first to leave a review!
        </div>
        <ul v-else class="space-y-6">
          <li v-for="review in reviews" :key="review.id" class="border-b border-gray-200 pb-6 last:border-b-0 last:pb-0">
            <div class="flex items-center mb-2">
              <div class="flex-shrink-0">
                <img :src="review.avatar" alt="User avatar" class="h-10 w-10 rounded-full">
              </div>
              <div class="ml-3">
                <p class="text-sm font-medium text-gray-900">{{ review.userName }}</p>
                <div class="flex items-center">
                  <StarIcon v-for="i in review.rating" :key="i" class="h-5 w-5 text-yellow-400" />
                  <StarIcon v-for="i in 5 - review.rating" :key="i + 5" class="h-5 w-5 text-gray-300" />
                </div>
              </div>
            </div>
            <p class="text-gray-700">{{ review.text }}</p>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>

</style>
