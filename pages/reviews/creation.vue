<script setup>
import { ref, computed, watch } from 'vue'
import { SendIcon, StarIcon, ChevronDownIcon, CheckIcon, Star } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue'

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
  date: new Date().toISOString().split('T')[0]
})


const rating = ref(0)
const hoverRating = ref(0)

const setRating = (value) => {
  rating.value = value
}

const setHoverRating = (value) => {
  hoverRating.value = value
}

const clearHoverRating = () => {
  hoverRating.value = 0
}

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

const formProgress = computed(() => {
  const requiredFields = [
    selectedCompany.value || newCompanyName.value,
    review.value.reviewerName,
    review.value.reviewText,
    review.value.rating
  ];
  const filledFields = requiredFields.filter(Boolean).length;
  return Math.round((filledFields / requiredFields.length) * 100);
})

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
    date: new Date().toISOString().split('T')[0]
  }
  selectedCompany.value = ''
  newCompanyName.value = ''
  showNewCompanyInput.value = false
  isAnonymous.value = false
}
</script>

<template>
  <Navigation />

  <div class="min-h-screen flex flex-col bg-gray-100 relative overflow-hidden">
    <!-- Main Content -->
    <main class="flex-grow relative z-10 bg-gradient-to-br from-indigo-50 to-blue-100">
      <div class="max-w-3xl mx-auto py-12 px-4 sm:px-6 lg:px-8">
        <div class="bg-white shadow-xl rounded-lg overflow-hidden">
          <div class="px-6 py-8">
            <h2 class="text-3xl font-extrabold text-gray-900 text-center">Create a New Review</h2>
            <p class="mt-2 text-center text-sm text-gray-600">
              Share your experience and help others make informed decisions
            </p>
          </div>

          <form @submit.prevent="submitReview" class="space-y-8 px-6 pb-8">

            <div class="mb-6">
              <div class="relative pt-1">
                <div class="flex mb-2 items-center justify-between">
                  <div>
                    <span class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-indigo-600 bg-indigo-200">
                      Progress
                    </span>
                  </div>
                  <div class="text-right">
                    <span class="text-xs font-semibold inline-block text-indigo-600">
                      {{ formProgress }}%
                    </span>
                  </div>
                </div>
                <div class="overflow-hidden h-2 mb-4 text-xs flex rounded bg-indigo-200">
                  <div :style="{ width: `${formProgress}%` }" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-indigo-500 transition-all duration-300 ease-in-out"></div>
                </div>
              </div>
            </div>

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
              <div class="flex items-center space-x-2">
                <template v-for="star in 5" :key="star">
                  <button
                    @click="setRating(star)"
                    @mouseenter="setHoverRating(star)"
                    @mouseleave="clearHoverRating"
                    class="transition-transform duration-200 ease-in-out transform hover:scale-110 focus:outline-none focus:ring-2 focus:ring-yellow-400 rounded-full"
                    :aria-label="`Rate ${star} stars`"
                  >
                    <Star
                      :class="[
                        'w-5 h-5 sm:w-8 sm:h-8',
                        (hoverRating || rating) >= star
                          ? 'text-yellow-400 fill-current'
                          : 'text-gray-300'
                      ]"
                    />
                  </button>
                </template>
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

<style>
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

button:focus Star {
  animation: pulse 0.5s ease-in-out;
}
</style>
