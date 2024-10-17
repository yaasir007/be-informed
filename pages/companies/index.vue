<script setup>
import { ref } from 'vue'
import { StarIcon } from 'lucide-vue-next'

const companies = ref([
  {
    id: 1,
    name: 'TechCorp',
    description: 'A leading technology company specializing in innovative software solutions for businesses of all sizes.',
    averageRating: 4.5
  },
  {
    id: 2,
    name: 'FinanceInc',
    description: 'Providing cutting-edge financial services and investment strategies to help clients achieve their financial goals.',
    averageRating: 4.2
  },
  {
    id: 3,
    name: 'RetailGiant',
    description: 'The largest online retailer offering a vast selection of products with fast and reliable delivery services.',
    averageRating: 4.7
  },
  {
    id: 4,
    name: 'HealthCare Co.',
    description: 'Dedicated to improving lives through advanced medical research and innovative healthcare solutions.',
    averageRating: 4.3
  },
  {
    id: 5,
    name: 'EcoEnergy',
    description: 'Pioneering sustainable energy solutions to combat climate change and reduce carbon footprints.',
    averageRating: 4.6
  },
  {
    id: 6,
    name: 'FoodDelight',
    description: 'Bringing gourmet meals and fresh ingredients directly to your doorstep with our meal kit delivery service.',
    averageRating: 4.1
  },
  {
    id: 6,
    name: 'HealthTech Innovations',
    description: 'Pioneering healthcare technology solutions to improve patient care and operational efficiency.',
    averageRating: 4.8
  },
  {
    id: 7,
    name: 'Green Energy Solutions',
    description: 'Leading the charge in renewable energy technologies for a sustainable future.',
    averageRating: 4.7
  },
  {
    id: 8,
    name: 'FinTech Dynamics',
    description: 'Revolutionizing financial services with cutting-edge software for better financial management.',
    averageRating: 4.6
  },
  {
    id: 9,
    name: 'EduTech Hub',
    description: 'Transforming education through innovative online learning platforms and tools.',
    averageRating: 4.9
  },
  {
    id: 10,
    name: 'RetailRevamp',
    description: 'Helping retail businesses thrive with advanced e-commerce solutions and analytics.',
    averageRating: 4.5
  },
  {
    id: 11,
    name: 'AI Solutions Inc.',
    description: 'Integrating artificial intelligence into business processes to drive efficiency and growth.',
    averageRating: 4.8
  },
  {
    id: 12,
    name: 'CloudSafe Systems',
    description: 'Providing robust cloud security solutions for data protection and compliance.',
    averageRating: 4.7
  },
  {
    id: 13,
    name: 'Agile DevOps',
    description: 'Delivering agile software development and operations solutions for faster product delivery.',
    averageRating: 4.6
  },
  {
    id: 14,
    name: 'Blockchain Ventures',
    description: 'Innovating with blockchain technology to enhance transparency and trust in transactions.',
    averageRating: 4.9
  },
  {
    id: 15,
    name: 'SmartCity Technologies',
    description: 'Creating smart solutions for urban development, improving infrastructure and quality of life.',
    averageRating: 4.7
  }
])
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

  <div class="min-h-screen bg-gray-100">
    <main>
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="px-4 py-6 sm:px-0">
          <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
            <div v-for="company in companies" :key="company.id" class="bg-white overflow-hidden shadow rounded-lg">
              <div class="px-4 py-5 sm:p-6">
                <h3 class="text-lg leading-6 font-medium text-gray-900">{{ company.name }}</h3>
                <div class="mt-2 max-w-xl text-sm text-gray-500">
                  <p>{{ company.description }}</p>
                </div>
                <div class="mt-3 flex items-center">
                  <div class="flex items-center">
                    <StarIcon v-for="i in 5" :key="i" :class="[
                      i <= Math.round(company.averageRating) ? 'text-yellow-400' : 'text-gray-300',
                      'h-5 w-5 flex-shrink-0'
                    ]" :fill="i <= Math.round(company.averageRating) ? 'currentColor' : 'none'" aria-hidden="true" />
                  </div>
                  <p class="ml-2 text-sm text-gray-700">{{ company.averageRating.toFixed(1) }} out of 5 stars</p>
                </div>
                <div class="mt-3 text-sm">
                  <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500">
                    View details<span class="sr-only"> for {{ company.name }}</span>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
