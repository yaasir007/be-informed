<script setup>
import { ref, computed } from 'vue'
import { BuildingIcon, BriefcaseIcon, GlobeIcon, MapPinIcon } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue';

const companyForm = ref({
  name: '',
  industry: '',
  website: '',
  headquarters: '',
  description: ''
})

const industries = [
  'Technology', 'Finance', 'Healthcare', 'Education', 'Retail',
  'Manufacturing', 'Entertainment', 'Food & Beverage', 'Transportation', 'Other'
]

const formProgress = computed(() => {
  const totalFields = Object.keys(companyForm.value).length
  const filledFields = Object.values(companyForm.value).filter(Boolean).length
  return Math.round((filledFields / totalFields) * 100)
})

const submitForm = () => {
  console.log('Submitting company:', companyForm.value)
  alert('Company added successfully!')
  companyForm.value = {
    name: '',
    industry: '',
    website: '',
    headquarters: '',
    description: ''
  }
}
</script>

<template>
  <Navigation />

  <div class="min-h-screen bg-gradient-to-br from-indigo-50 to-blue-100 py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <div class="bg-white shadow-lg rounded-lg overflow-hidden">
        <div class="px-4 py-5 sm:p-6">
          <h2 class="text-3xl font-extrabold text-gray-900 mb-6">Add a New Company</h2>
          <div class="mb-6">
            <div class="relative pt-1">
              <div class="flex mb-2 items-center justify-between">
                <div>
                  <span v-if="formProgress !== 100" class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-indigo-600 bg-indigo-200">
                    Progress
                  </span>
                  <span v-else class="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-green-600 bg-green-200">
                    Progress
                  </span>
                </div>
                <div class="text-right">
                  <span v-if="formProgress !== 100" class="text-xs font-semibold inline-block text-indigo-600">
                    {{ formProgress }}%
                  </span>
                  <span v-else class="text-xs font-semibold inline-block text-green-600">
                    {{ formProgress }}%
                  </span>
                </div>
              </div>
              <div class="overflow-hidden h-1 mb-4 text-xs flex rounded bg-indigo-200">
                <div v-if="formProgress !== 100" :style="{ width: `${formProgress}%` }" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-indigo-500 transition-all duration-300 ease-in-out"></div>
                <div v-else :style="{ width: `${formProgress}%` }" class="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-green-500 transition-all duration-300 ease-in-out"></div>
              </div>
            </div>
          </div>
          <form @submit.prevent="submitForm" class="space-y-8">
            <div class="grid grid-cols-1 gap-y-6 gap-x-4 sm:grid-cols-2">
              <div class="sm:col-span-2">
                <label for="company-name" class="block text-sm font-medium text-gray-700">Company Name</label>
                <div class="mt-1 relative rounded-md shadow-sm">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <BuildingIcon class="h-5 w-5 text-gray-400" />
                  </div>
                  <input
                    type="text"
                    name="company-name"
                    id="company-name"
                    v-model="companyForm.name"
                    required
                    class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-10 pr-3 py-2 sm:text-sm border-gray-300 rounded-md transition duration-150 ease-in-out"
                    placeholder="Enter company name"
                  >
                </div>
              </div>

              <div>
                <label for="industry" class="block text-sm font-medium text-gray-700">Industry</label>
                <div class="mt-1 relative rounded-md shadow-sm">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <BriefcaseIcon class="h-5 w-5 text-gray-400" />
                  </div>
                  <select
                    id="industry"
                    name="industry"
                    v-model="companyForm.industry"
                    required
                    class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-10 pr-10 py-2 sm:text-sm border-gray-300 rounded-md appearance-none transition duration-150 ease-in-out"
                  >
                    <option value="">Select an industry</option>
                    <option v-for="industry in industries" :key="industry" :value="industry">
                      {{ industry }}
                    </option>
                  </select>
                  <div class="absolute inset-y-0 right-0 flex items-center px-2 pointer-events-none">
                    <svg class="h-5 w-5 text-gray-400" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                      <path fill-rule="evenodd" d="M10 3a1 1 0 01.707.293l3 3a1 1 0 01-1.414 1.414L10 5.414 7.707 7.707a1 1 0 01-1.414-1.414l3-3A1 1 0 0110 3zm-3.707 9.293a1 1 0 011.414 0L10 14.586l2.293-2.293a1 1 0 011.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z" clip-rule="evenodd" />
                    </svg>
                  </div>
                </div>
              </div>

              <div>
                <label for="website" class="block text-sm font-medium text-gray-700">Website</label>
                <div class="mt-1 relative rounded-md shadow-sm">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <GlobeIcon class="h-5 w-5 text-gray-400" />
                  </div>
                  <input
                    type="url"
                    name="website"
                    id="website"
                    v-model="companyForm.website"
                    class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-10 pr-3 py-2 sm:text-sm border-gray-300 rounded-md transition duration-150 ease-in-out"
                    placeholder="https://example.com"
                  >
                </div>
              </div>

              <div>
                <label for="headquarters" class="block text-sm font-medium text-gray-700">Headquarters</label>
                <div class="mt-1 relative rounded-md shadow-sm">
                  <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                    <MapPinIcon class="h-5 w-5 text-gray-400" />
                  </div>
                  <input
                    type="text"
                    name="headquarters"
                    id="headquarters"
                    v-model="companyForm.headquarters"
                    class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-10 pr-3 py-2 sm:text-sm border-gray-300 rounded-md transition duration-150 ease-in-out"
                    placeholder="City, Country"
                  >
                </div>
              </div>

              <div class="sm:col-span-2">
                <label for="description" class="block text-sm font-medium text-gray-700">Company Description</label>
                <div class="mt-1">
                  <textarea
                    id="description"
                    name="description"
                    rows="4"
                    v-model="companyForm.description"
                    class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md transition duration-150 ease-in-out p-2"
                    placeholder="Provide a brief description of the company"
                  ></textarea>
                </div>
              </div>
            </div>

            <div>
              <button
                type="submit"
                class="w-full inline-flex justify-center items-center px-6 py-3 border border-transparent text-base font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
              >
                <span>Add Company</span>
                <svg class="ml-2 -mr-1 h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                  <path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd" />
                </svg>
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Add any component-specific styles here if needed */
.transition-all {
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}

.hover\:scale-105:hover {
  transform: scale(1.05);
}
</style>
