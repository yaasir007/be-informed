<script setup>
import { ref, computed } from 'vue'
import { StarIcon, ThumbsUpIcon, ChevronDownIcon, FolderOpenIcon, CheckIcon, PlusIcon } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue'

// Mock data
const username = ref('John Doe')
const companies = ['TechCorp', 'FinanceInc', 'RetailGiant', 'HealthCare Co.']
const allReviews = [
  { id: 1, companyName: 'TechCorp', reviewerName: 'Alice Johnson', date: '2023-05-15', rating: 4, reviewText: 'Great work environment with lots of opportunities for growth.', helpfulVotes: 12 },
  { id: 2, companyName: 'FinanceInc', reviewerName: 'Bob Smith', date: '2023-05-10', rating: 3, reviewText: 'Good benefits but high-stress environment.', helpfulVotes: 8 },
  { id: 3, companyName: 'RetailGiant', reviewerName: 'Carol Williams', date: '2023-05-05', rating: 5, reviewText: 'Excellent company culture and work-life balance.', helpfulVotes: 15 },
  { id: 4, companyName: 'TechCorp', reviewerName: 'David Brown', date: '2023-04-30', rating: 2, reviewText: 'Long hours and limited growth opportunities.', helpfulVotes: 6 },
  { id: 5, companyName: 'HealthCare Co.', reviewerName: 'Eva Martinez', date: '2023-04-25', rating: 4, reviewText: 'Meaningful work and supportive management.', helpfulVotes: 10 },
  { id: 6, companyName: 'FinanceInc', reviewerName: 'Frank Lee', date: '2023-04-20', rating: 4, reviewText: 'Competitive salary and great learning opportunities.', helpfulVotes: 9 },
  { id: 7, companyName: 'RetailGiant', reviewerName: 'Grace Kim', date: '2023-04-15', rating: 2, reviewText: 'Challenging work schedule and limited advancement.', helpfulVotes: 7 },
  { id: 8, companyName: 'TechCorp', reviewerName: 'Henry Wilson', date: '2023-04-10', rating: 5, reviewText: 'Innovative projects and collaborative team environment.', helpfulVotes: 14 },
]

const selectedCompany = ref('')
const sortBy = ref('recent')
const visibleReviews = ref(3)
const isDropdownOpen = ref({ company: false, sort: false })

const sortOptions = {
  recent: 'Most Recent',
  'rating-high': 'Highest Rating',
  'rating-low': 'Lowest Rating'
}

const filteredAndSortedReviews = computed(() => {
  let filtered = selectedCompany.value
    ? allReviews.filter(review => review.companyName === selectedCompany.value)
    : allReviews

  switch (sortBy.value) {
    case 'rating-high':
      return filtered.sort((a, b) => b.rating - a.rating)
    case 'rating-low':
      return filtered.sort((a, b) => a.rating - b.rating)
    case 'recent':
    default:
      return filtered.sort((a, b) => new Date(b.date) - new Date(a.date))
  }
})

const filteredReviews = computed(() => {
  return filteredAndSortedReviews.value.slice(0, visibleReviews.value)
})

const hasMoreReviews = computed(() => {
  return visibleReviews.value < filteredAndSortedReviews.value.length
})

const formatDate = (dateString) => {
  const options = { year: 'numeric', month: 'long', day: 'numeric' }
  return new Date(dateString).toLocaleDateString(undefined, options)
}

const loadMore = () => {
  visibleReviews.value += 3
}

const resetVisibleReviews = () => {
  visibleReviews.value = 3
}

const toggleDropdown = (type) => {
  isDropdownOpen.value[type] = !isDropdownOpen.value[type]
  // Close the other dropdown
  const otherType = type === 'company' ? 'sort' : 'company'

  isDropdownOpen.value[otherType] = false
}

const selectCompany = (company) => {
  selectedCompany.value = company
  isDropdownOpen.value.company = false
  resetVisibleReviews()
}

const selectSort = (sort) => {
  sortBy.value = sort
  isDropdownOpen.value.sort = false
  resetVisibleReviews()
}

const logout = () => {
  console.log('Logging out...')
}
</script>


<template>
  <Navigation />

  <div class="min-h-screen bg-gradient-to-br from-indigo-50 to-blue-100 py-6">
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="mb-3 flex flex-col sm:flex-row justify-between items-start sm:items-center">
        <NuxtLink to="../reviews/creation" class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
          <PlusIcon class="h-5 w-5 mr-2" />
          Create Review
        </NuxtLink>
      </div>

      <div class="bg-white shadow rounded-lg p-6 mb-6">
        <div class="flex flex-col md:flex-row md:items-end space-y-4 md:space-y-0 md:space-x-4">
          <div class="flex-grow">
            <label for="company-filter" class="block text-sm font-medium text-gray-700 mb-1">Filter by Company</label>
            <div class="relative">
              <button
                @click="toggleDropdown('company')"
                class="w-full bg-white border border-gray-300 rounded-md py-2 pl-3 pr-10 text-left cursor-default focus:outline-none focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                aria-haspopup="listbox"
                :aria-expanded="isDropdownOpen.company"
              >
                <span class="block truncate">{{ selectedCompany || 'All Companies' }}</span>
                <span class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                  <ChevronDownIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
                </span>
              </button>
              <transition
                enter-active-class="transition ease-out duration-100"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <ul
                  v-if="isDropdownOpen.company"
                  class="absolute z-10 mt-1 w-full bg-white shadow-lg max-h-60 rounded-md py-1 text-base ring-1 ring-black ring-opacity-5 overflow-auto focus:outline-none sm:text-sm"
                  tabindex="-1"
                  role="listbox"
                >
                  <li
                    class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-indigo-50"
                    @click="selectCompany('')"
                    :class="{ 'bg-indigo-100': selectedCompany === '' }"
                  >
                    <span class="block truncate">All Companies</span>
                    <span v-if="selectedCompany === ''" class="absolute inset-y-0 right-0 flex items-center pr-4 text-indigo-600">
                      <CheckIcon class="h-5 w-5" aria-hidden="true" />
                    </span>
                  </li>
                  <li
                    v-for="company in companies"
                    :key="company"
                    class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-indigo-50"
                    @click="selectCompany(company)"
                    :class="{ 'bg-indigo-100': selectedCompany === company }"
                  >
                    <span class="block truncate">{{ company }}</span>
                    <span v-if="selectedCompany === company" class="absolute inset-y-0 right-0 flex items-center pr-4 text-indigo-600">
                      <CheckIcon class="h-5 w-5" aria-hidden="true" />
                    </span>
                  </li>
                </ul>
              </transition>
            </div>
          </div>
          <div class="w-full md:w-48">
            <label for="sort-by" class="block text-sm font-medium text-gray-700 mb-1">Sort by</label>
            <div class="relative">
              <button
                @click="toggleDropdown('sort')"
                class="w-full bg-white border border-gray-300 rounded-md py-2 pl-3 pr-10 text-left cursor-default focus:outline-none focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                aria-haspopup="listbox"
                :aria-expanded="isDropdownOpen.sort"
              >
                <span class="block truncate">{{ sortOptions[sortBy] }}</span>
                <span class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none">
                  <ChevronDownIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
                </span>
              </button>
              <transition
                enter-active-class="transition ease-out duration-100"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <ul
                  v-if="isDropdownOpen.sort"
                  class="absolute z-10 mt-1 w-full bg-white shadow-lg max-h-60 rounded-md py-1 text-base ring-1 ring-black ring-opacity-5 overflow-auto focus:outline-none sm:text-sm"
                  tabindex="-1"
                  role="listbox"
                >
                  <li
                    v-for="(label, value) in sortOptions"
                    :key="value"
                    class="text-gray-900 cursor-default select-none relative py-2 pl-3 pr-9 hover:bg-indigo-50"
                    @click="selectSort(value)"
                    :class="{ 'bg-indigo-100': sortBy === value }"
                  >
                    <span class="block truncate">{{ label }}</span>
                    <span v-if="sortBy === value" class="absolute inset-y-0 right-0 flex items-center pr-4 text-indigo-600">
                      <CheckIcon class="h-5 w-5" aria-hidden="true" />
                    </span>
                  </li>
                </ul>
              </transition>
            </div>
          </div>
        </div>
      </div>

      <TransitionGroup
        name="review-list"
        tag="div"
        class="space-y-6"
      >
        <div v-if="filteredReviews.length === 0" key="empty-state" class="text-center py-12">
          <FolderOpenIcon class="mx-auto h-12 w-12 text-gray-400" />
          <h3 class="mt-2 text-sm font-medium text-gray-900">No reviews found</h3>
          <p class="mt-1 text-sm text-gray-500">There are no reviews for the selected company.</p>
        </div>

        <div v-for="review in filteredReviews" :key="review.id" class="bg-white shadow overflow-hidden sm:rounded-lg">
          <div class="px-4 py-5 sm:px-6">
            <h3 class="text-lg leading-6 font-medium text-gray-900">
              {{ review.companyName }}
            </h3>
            <p class="mt-1 max-w-2xl text-sm text-gray-500">
              Review by {{ review.reviewerName }} on {{ formatDate(review.date) }}
            </p>
          </div>
          <div class="border-t border-gray-200 px-4 py-5 sm:px-6">
            <div class="flex items-center mb-2">
              <div class="flex items-center">
                <StarIcon v-for="i in 5" :key="i" :class="[i <= review.rating ? 'text-yellow-400' : 'text-gray-300', 'h-5 w-5 flex-shrink-0']" :fill="i <= review.rating ? 'currentColor' : 'none'" />
              </div>
              <p class="ml-2 text-sm text-gray-500">{{ review.rating }} out of 5 stars</p>
            </div>
            <p class="text-sm text-gray-500">{{ review.reviewText }}</p>
            <div class="mt-4 flex items-center">
              <ThumbsUpIcon class="h-5 w-5 text-gray-400 mr-1" />
              <span class="text-sm text-gray-500">{{ review.helpfulVotes }} found this helpful</span>
            </div>
          </div>
        </div>
      </TransitionGroup>

      <Transition name="fade">
        <div v-if="hasMoreReviews" class="mt-6 flex justify-center">
          <button @click="loadMore" class="bg-white hover:bg-gray-50 text-gray-700 font-semibold py-2 px-4 border border-gray-300 rounded shadow transition duration-300 ease-in-out transform hover:scale-105">
            Load More
          </button>
        </div>
      </Transition>
    </main>
  </div>
</template>

<style scoped>
.review-list-move,
.review-list-enter-active,
.review-list-leave-active {
  transition: all 0.5s ease;
}

.review-list-enter-from,
.review-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.review-list-leave-active {
  position: absolute;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
