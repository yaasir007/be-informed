<script setup lang="ts">
import { ref } from 'vue'
import { SearchIcon, StarIcon, PenIcon, FacebookIcon, TwitterIcon, LinkedinIcon, MenuIcon, XIcon } from 'lucide-vue-next'

const email = ref('')
const mobileMenuOpen = ref(false)

const testimonials = [
  {
    id: 1,
    name: 'Alice Johnson',
    position: 'Software Engineer',
    avatar: XIcon,
    quote: 'This platform helped me find a company that aligns with my values. The reviews were spot-on!'
  },
  {
    id: 2,
    name: 'Bob Smith',
    position: 'Marketing Manager',
    avatar: XIcon,
    quote: 'I love how easy it is to share my experiences and help others make informed career decisions.'
  },
  {
    id: 3,
    name: 'Carol Williams',
    position: 'HR Specialist',
    avatar: XIcon,
    quote: 'As an HR professional, I find the insights from this platform invaluable for improving our workplace.'
  }
]

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const subscribeNewsletter = () => {
  // Here you would typically send the email to your backend
  console.log('Subscribing email:', email.value)
  // Reset form
  email.value = ''
  // You might want to show a success message to the user here
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Navigation -->
    <nav class="bg-white shadow">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-16">
          <div class="flex">
            <div class="flex-shrink-0 flex items-center">
              <span class="ml-2 text-xl font-bold text-[#4F45E4]">BeInformed</span>
            </div>
          </div>
          <div class="hidden sm:ml-6 sm:flex sm:space-x-8">
            <NuxtLink to="./" class="border-indigo-500 text-gray-900 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Home</NuxtLink>
            <NuxtLink to="./companies" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Companies</NuxtLink>
            <NuxtLink to="./reviews" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">Reviews</NuxtLink>
            <NuxtLink to="./" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">About</NuxtLink>
          </div>
          <div class="hidden sm:ml-6 sm:flex sm:items-center">
            <NuxtLink to="../auth/login" class="bg-indigo-600 text-white px-4 py-2 rounded-md text-sm font-medium hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
              Sign In
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

    <!-- Hero Section -->
    <header class="bg-indigo-600">
      <div class="max-w-7xl mx-auto py-16 px-4 sm:px-6 lg:px-8 flex flex-col lg:flex-row items-center">
        <div class="lg:w-1/2 text-center lg:text-left">
          <h1 class="text-4xl font-extrabold text-white sm:text-5xl md:text-6xl">
            Find Your Perfect Company
          </h1>
          <p class="mt-3 text-base text-indigo-200 sm:mt-5 sm:text-xl lg:text-lg xl:text-xl">
            Read honest reviews from employees and make informed career decisions.
          </p>
          <div class="mt-8 sm:flex sm:justify-center lg:justify-start">
            <div class="rounded-md shadow">
              <a href="#" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-indigo-600 bg-white hover:bg-indigo-50 md:py-4 md:text-lg md:px-10">
                Get Started
              </a>
            </div>
            <div class="mt-3 sm:mt-0 sm:ml-3">
              <a href="#" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-indigo-500 hover:bg-indigo-600 md:py-4 md:text-lg md:px-10">
                Read Reviews
              </a>
            </div>
          </div>
        </div>
        <div class="lg:w-1/2 mt-10 lg:mt-0">
          <img class="w-full" src="/assets/images/hero-section.jpg" alt="Company reviews illustration">
        </div>
      </div>
    </header>

    <!-- How It Works Section -->
    <section class="py-16 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 class="text-3xl font-extrabold text-gray-900 text-center mb-12">
          How It Works
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="text-center">
            <div class="bg-indigo-100 rounded-full w-16 h-16 flex items-center justify-center mx-auto mb-4">
              <SearchIcon class="w-8 h-8 text-indigo-600" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Find Companies</h3>
            <p class="text-gray-600">Search for companies you're interested in or have worked for.</p>
          </div>
          <div class="text-center">
            <div class="bg-indigo-100 rounded-full w-16 h-16 flex items-center justify-center mx-auto mb-4">
              <StarIcon class="w-8 h-8 text-indigo-600" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Read Reviews</h3>
            <p class="text-gray-600">Get insights from current and former employees.</p>
          </div>
          <div class="text-center">
            <div class="bg-indigo-100 rounded-full w-16 h-16 flex items-center justify-center mx-auto mb-4">
              <PenIcon class="w-8 h-8 text-indigo-600" />
            </div>
            <h3 class="text-xl font-semibold mb-2">Share Your Experience</h3>
            <p class="text-gray-600">Help others by leaving your own review.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section class="py-16 bg-gray-100">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 class="text-3xl font-extrabold text-gray-900 text-center mb-12">
          What Our Users Say
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="testimonial in testimonials" :key="testimonial.id" class="bg-white p-6 rounded-lg shadow-md">
            <div class="flex items-center mb-4">
              <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTOuxrvcNMfGLh73uKP1QqYpKoCB0JLXiBMvA&s" :alt="testimonial.name" class="w-12 h-12 rounded-full mr-4">
              <div>
                <h3 class="font-semibold text-lg">{{ testimonial.name }}</h3>
                <p class="text-gray-600">{{ testimonial.position }}</p>
              </div>
            </div>
            <p class="text-gray-700">{{ testimonial.quote }}</p>
          </div>
        </div>
      </div>
    </section>

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
  </div>
</template>

<style lang="scss" scoped>

</style>
