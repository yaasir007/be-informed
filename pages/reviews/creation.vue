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
          <a href="/" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">
            Companies
          </a>
          <NuxtLink to="../reviews" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Reviews</NuxtLink>
          <a href="#" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">
            About
          </a>
        </div>
        <div class="hidden sm:ml-6 sm:flex sm:items-center">
          <NuxtLink to="../auth/login" class="bg-indigo-600 text-white px-4 py-2 rounded-md text-sm font-medium hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            Log out
          </NuxtLink>
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

  <div class="min-h-screen flex flex-col bg-gray-100 relative overflow-hidden">
    <!-- Animated Background -->
    <div class="absolute inset-0 z-0">
      <div v-for="i in 10" :key="i"
        class="absolute rounded-full opacity-10 animate-float"
        :style="{
          width: `${Math.random() * 300 + 50}px`,
          height: `${Math.random() * 300 + 50}px`,
          left: `${Math.random() * 100}%`,
          top: `${Math.random() * 100}%`,
          animationDelay: `${Math.random() * 3}s`,
          backgroundColor: ['#4F46E5', '#818CF8', '#6366F1'][Math.floor(Math.random() * 3)]
        }"
      ></div>
    </div>

    <!-- Main Content -->
    <main class="flex-grow relative z-10">
      <div class="max-w-2xl mx-auto py-12 px-4 sm:px-6 lg:px-8">
        <div class="bg-white shadow-xl rounded-lg overflow-hidden">
          <div class="px-6 py-8">
            <h2 class="text-3xl font-extrabold text-gray-900 text-center">Create a New Review</h2>
            <p class="mt-2 text-center text-sm text-gray-600">
              Share your experience and help others make informed decisions
            </p>
          </div>

          <form @submit.prevent="submitReview" class="space-y-8 px-6 pb-8">
            <!-- Company Selection -->
            <div class="space-y-2">
              <label for="company-select" class="block text-sm font-medium text-gray-700">Company Name</label>
              <div class="relative">
                <button
                  type="button"
                  @click="toggleDropdown"
                  class="relative w-full bg-white border border-gray-300 rounded-md shadow-sm pl-3 pr-10 py-2 text-left cursor-default focus:outline-none focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                  aria-haspopup="listbox"
                  :aria-expanded="isOpen"
                >
                  <span class="block truncate">{{ selectedCompany || 'Select a company' }}</span>
                  <span class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                    <ChevronDownIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
                  </span>
                </button>

                <transition
                  leave-active-class="transition ease-in duration-100"
                  leave-from-class="opacity-100"
                  leave-to-class="opacity-0"
                >
                  <ul
                    v-if="isOpen"
                    class="absolute z-10 mt-1 w-full bg-white shadow-lg max-h-60 rounded-md py-1 text-base ring-1 ring-black ring-opacity-5 overflow-auto focus:outline-none sm:text-sm"
                    tabindex="-1"
                    role="listbox"
                  >
                    <li
                      v-for="company in companies"
                      :key="company"
                      class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-indigo-50"
                      :class="{ 'bg-indigo-50': company === selectedCompany }"
                      @click="selectCompany(company)"
                      role="option"
                    >
                      <span class="block truncate" :class="{ 'font-semibold': company === selectedCompany }">
                        {{ company }}
                      </span>
                      <span
                        v-if="company === selectedCompany"
                        class="absolute inset-y-0 right-0 flex items-center pr-4 text-indigo-600"
                      >
                        <CheckIcon class="h-5 w-5" aria-hidden="true" />
                      </span>
                    </li>
                    <li
                      class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-indigo-50"
                      @click="selectNewCompany"
                      role="option"
                    >
                      <span class="block truncate font-medium text-indigo-600">
                        + Add new company
                      </span>
                    </li>
                  </ul>
                </transition>
              </div>
            </div>

            <!-- New Company Input -->
            <div v-if="showNewCompanyInput" class="space-y-2">
              <label for="new-company-name" class="block text-sm font-medium text-gray-700">New Company Name</label>
              <input
                id="new-company-name"
                v-model="newCompanyName"
                type="text"
                required
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                placeholder="Enter new company name"
              >
            </div>

            <!-- Reviewer Name Section -->
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <label for="reviewer-name" class="block text-sm font-medium text-gray-700">Your Name</label>
                <div class="flex items-center">
                  <input
                    id="anonymous-review"
                    v-model="isAnonymous"
                    type="checkbox"
                    class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded"
                  >
                  <label for="anonymous-review" class="ml-2 block text-sm text-gray-900">
                    Post anonymously
                  </label>
                </div>
              </div>
              <input
                id="reviewer-name"
                v-model="review.reviewerName"
                type="text"
                :disabled="isAnonymous"
                :required="!isAnonymous"
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                :class="{ 'bg-gray-100': isAnonymous }"
                placeholder="Your Name"
              >
            </div>

            <!-- Review Title -->
            <div class="space-y-2">
              <label for="review-title" class="block text-sm font-medium text-gray-700">Review Title</label>
              <input
                id="review-title"
                v-model="review.title"
                type="text"
                required
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                placeholder="Summarize your experience"
              >
            </div>

            <!-- Review Text -->
            <div class="space-y-2">
              <label for="review-text" class="block text-sm font-medium text-gray-700">Your Review</label>
              <textarea
                id="review-text"
                v-model="review.reviewText"
                rows="6"
                required
                class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                placeholder="Write your review here..."
              ></textarea>
            </div>

            <!-- Star Rating -->
            <div class="space-y-2">
              <label for="star-rating" class="block text-sm font-medium text-gray-700">Your Rating</label>
              <StarRating v-model="review.rating" id="star-rating" />
            </div>

            <!-- Pros and Cons -->
            <div class="space-y-4">
              <div class="space-y-2">
                <label for="pros" class="block text-sm font-medium text-gray-700">Pros</label>
                <textarea
                  id="pros"
                  v-model="review.pros"
                  rows="3"
                  class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                  placeholder="What did you like about this company?"
                ></textarea>
              </div>
              <div class="space-y-2">
                <label for="cons" class="block text-sm font-medium text-gray-700">Cons</label>
                <textarea
                  id="cons"
                  v-model="review.cons"
                  rows="3"
                  class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                  placeholder="What could be improved?"
                ></textarea>
              </div>
            </div>

            <!-- Submit Button -->
            <div>
              <button
                type="submit"
                class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition duration-150 ease-in-out"
              >
                <SendIcon class="h-5 w-5 mr-2" />
                Submit Review
              </button>
            </div>
          </form>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import { SendIcon, StarIcon, ChevronDownIcon, CheckIcon } from 'lucide-vue-next'

const companies = ['TechCorp', 'FinanceInc', 'RetailGiant', 'HealthCare Co.']
const selectedCompany = ref('')
const newCompanyName = ref('')
const showNewCompanyInput = ref(false)
const isOpen = ref(false)
const isAnonymous = ref(false)

const review = ref({
  companyName: '',
  reviewerName: '',
  title: '',
  reviewText: '',
  rating: 0,
  pros: '',
  cons: '',
  date: new Date().toISOString().split('T')[0]
})

watch(isAnonymous, (newValue) => {
  if (newValue) {
    review.value.reviewerName = 'Anonymous'
  } else {
    review.value.reviewerName = ''
  }
})

const toggleDropdown = () => {
  isOpen.value = !isOpen.value
}

const selectCompany = (company) => {
  selectedCompany.value = company
  review.value.companyName = company
  showNewCompanyInput.value = false
  isOpen.value = false
}

const selectNewCompany = () => {
  selectedCompany.value = ''
  showNewCompanyInput.value = true
  isOpen.value = false
}

const submitReview = () => {
  if (showNewCompanyInput.value) {
    review.value.companyName = newCompanyName.value
  }

  if (isAnonymous.value) {
    review.value.reviewerName = 'Anonymous'
  }

  console.log('Submitting review:', review.value)

  alert('Thank you for your review!')

  review.value = {
    companyName: '',
    reviewerName: '',
    title: '',
    reviewText: '',
    rating: 0,
    pros: '',
    cons: '',
    date: new Date().toISOString().split('T')[0]
  }
  selectedCompany.value = ''
  newCompanyName.value = ''
  showNewCompanyInput.value = false
  isAnonymous.value = false
}

const StarRating = {
  props: {
    modelValue: {
      type: Number,
      default: 0
    }
  },
  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const hoverRating = ref(0)

    const updateRating = (rating) => {
      emit('update:modelValue', rating)
    }

    return { hoverRating, updateRating }
  },
  template: `
    <div class="flex items-center space-x-1">
      <template v-for="star in 5" :key="star">
        <button
          @click="updateRating(star)"
          @mouseenter="hoverRating = star"
          @mouseleave="hoverRating = 0"
          class="focus:outline-none transition-colors duration-200"
          :aria-label="'Rate ' + star + ' stars'"
        >
          <StarIcon
            :class="[
              star <= (hoverRating || modelValue) ? 'text-yellow-400' : 'text-gray-300',
              'h-8 w-8'
            ]"
            :fill="star <= (hoverRating || modelValue) ? 'currentColor' : 'none'"
          />
        </button>
      </template>
    </div>
  `
}
</script>

<style>
@keyframes float {
  0% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-40px);
  }
  100% {
    transform: translateY(0px);
  }
}

.animate-float {
  animation: float 5s ease-in-out infinite;
}
</style>
