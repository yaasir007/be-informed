<script setup lang="ts">
import { ref } from 'vue'
import { SearchIcon, StarIcon, PenIcon, BriefcaseIcon, TrendingUpIcon, ShieldIcon, ChevronDownIcon, XIcon } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue'
import Footer from '@/pages/footer/index.vue'

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
  },
  {
    id: 4,
    name: 'Bob Smith',
    position: 'Marketing Manager',
    avatar: XIcon,
    quote: 'I love how easy it is to share my experiences and help others make informed career decisions.'
  },
  {
    id: 5,
    name: 'Carol Williams',
    position: 'HR Specialist',
    avatar: XIcon,
    quote: 'As an HR professional, I find the insights from this platform invaluable for improving our workplace.'
  }
]

const features = [
  { icon: BriefcaseIcon, title: 'Company Profiles', description: 'Detailed information on thousands of companies across various industries.' },
  { icon: StarIcon, title: 'Ratings & Reviews', description: 'Honest feedback from current and former employees on company culture, work-life balance, and more.' },
  { icon: TrendingUpIcon, title: 'Salary Insights', description: 'Up-to-date salary information to help you negotiate better compensation packages.' },
  { icon: ShieldIcon, title: 'Anonymous Reviews', description: 'Share your experiences without fear, thanks to our robust anonymity protections.' }
]

const faqItems = ref([
  {
    question: 'How do you ensure the authenticity of reviews?',
    answer: 'We use a combination of advanced algorithms and human moderation to verify the authenticity of all reviews. We also have strict policies against fake reviews and take immediate action when violations are detected.',
    isOpen: false
  },
  {
    question: 'Can companies respond to reviews?',
    answer: 'Yes, verified company representatives can respond to reviews. This allows for a balanced perspective and gives companies the opportunity to address feedback constructively.',
    isOpen: false
  },
  {
    question: 'How often is salary data updated?',
    answer: 'Our salary data is updated in real-time as new information is submitted by users. We also conduct regular audits to ensure the accuracy and relevance of our salary insights.',
    isOpen: false
  }
])

const toggleFAQ = (index: number) => {
  faqItems.value[index].isOpen = !faqItems.value[index].isOpen
}
</script>

<template>
  <div class="min-h-screen bg-gray-50">
    <!-- Nav Section -->
    <Navigation />

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
              <NuxtLink to="./auth/login" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-indigo-600 bg-white hover:bg-indigo-50 md:py-4 md:text-lg md:px-10">
                Get Started
              </NuxtLink>
            </div>
            <div class="mt-3 sm:mt-0 sm:ml-3">
              <NuxtLink to="./reviews" class="w-full flex items-center justify-center px-8 py-3 border border-transparent text-base font-medium rounded-md text-white bg-indigo-500 hover:bg-indigo-600 md:py-4 md:text-lg md:px-10">
                Read Reviews
              </NuxtLink>
            </div>
          </div>
        </div>
        <div class="lg:w-1/2 mt-10 lg:mt-0">
          <img class="w-full" src="/assets/images/hero-section.jpg" alt="Company reviews illustration">
        </div>
      </div>
    </header>

    <!-- How It Works Section -->
    <div class="py-16 bg-white">
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
    </div>

    <!-- Features Section -->
    <div class="py-16 bg-gray-100">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 class="text-3xl font-extrabold text-gray-900 text-center mb-12">
          Why Choose BeInformed
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
          <div v-for="feature in features" :key="feature.title" class="flex items-start">
            <div class="flex-shrink-0">
              <component :is="feature.icon" class="h-6 w-6 text-indigo-600" />
            </div>
            <div class="ml-4">
              <h3 class="text-lg font-medium text-gray-900">{{ feature.title }}</h3>
              <p class="mt-2 text-base text-gray-500">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Testimonials Section -->
    <div class="py-16 bg-white">
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
    </div>

    <!-- FAQ Section -->
    <div class="py-16 bg-gray-100">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <h2 class="text-3xl font-extrabold text-gray-900 text-center mb-12">
          Frequently Asked Questions
        </h2>
        <div class="space-y-8">
          <div v-for="(item, index) in faqItems" :key="index" class="bg-white shadow overflow-hidden sm:rounded-lg">
            <button @click="toggleFAQ(index)" class="px-4 py-5 sm:px-6 w-full text-left focus:outline-none">
              <h3 class="text-lg leading-6 font-medium text-gray-900 flex justify-between items-center">
                {{ item.question }}
                <ChevronDownIcon :class="{ 'transform rotate-180': item.isOpen }" class="h-5 w-5  text-gray-500" />
              </h3>
            </button>
            <div v-show="item.isOpen" class="px-4 py-5 sm:px-6 border-t border-gray-200">
              <p class="text-base text-gray-500">{{ item.answer }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- CTA Section -->
    <div class="bg-indigo-700">
      <div class="max-w-2xl mx-auto text-center py-16 px-4 sm:py-20 sm:px-6 lg:px-8">
        <h2 class="text-3xl font-extrabold text-white sm:text-4xl">
          <span class="block">Ready to make informed career decisions?</span>
          <span class="block">Start exploring company reviews today.</span>
        </h2>
        <p class="mt-4 text-lg leading-6 text-indigo-200">
          Join thousands of professionals who are making smarter career choices with BeInformed.
        </p>
        <NuxtLink to="./auth/signup" class="mt-8 w-full inline-flex items-center justify-center px-5 py-3 border border-transparent text-base font-medium rounded-md text-indigo-600 bg-white hover:bg-indigo-50 sm:w-auto">Sign Up for Free</NuxtLink>
      </div>
    </div>

    <!-- Footer -->
    <Footer />
  </div>
</template>

<style lang="scss" scoped>

</style>
