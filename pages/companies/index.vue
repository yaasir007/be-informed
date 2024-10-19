<script setup>
import { ref } from 'vue'
import { StarIcon, PlusIcon } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue';

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
  <Navigation />

  <div class="min-h-screen bg-gray-100">
    <main>
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="px-4 py-6 sm:px-0">
          <div class="mb-3 flex flex-col sm:flex-row justify-between items-start sm:items-center">
            <NuxtLink to="./companies/creation" class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
              <PlusIcon class="h-5 w-5 mr-2" />
              Create Company
            </NuxtLink>
          </div>
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
