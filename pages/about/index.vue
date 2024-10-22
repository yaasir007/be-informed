<script setup>
import { ref, onMounted } from 'vue'
import { Lightbulb, Users, Shield } from 'lucide-vue-next'
import Navigation from '@/pages/navigation/index.vue'
import Footer from '@/pages/footer/index.vue'
import TeamPhoto from '@/assets/images/team_photo.jpg'

const teamMembers = [
  { id: 1, name: 'Jane Doe', position: 'CEO', bio: 'Visionary leader with 15+ years of industry experience.', image: '/placeholder.svg?height=400&width=300' },
  { id: 2, name: 'John Smith', position: 'CTO', bio: 'Tech guru passionate about cutting-edge innovations.', image: '/placeholder.svg?height=400&width=300' },
  { id: 3, name: 'Emily Brown', position: 'COO', bio: 'Operations expert ensuring smooth company processes.', image: '/placeholder.svg?height=400&width=300' },
]

const companyValues = [
  { id: 1, title: 'Innovation', description: 'We constantly push boundaries to create groundbreaking solutions.', icon: Lightbulb },
  { id: 2, title: 'Collaboration', description: 'We believe in the power of teamwork and diverse perspectives.', icon: Users },
  { id: 3, title: 'Integrity', description: 'We uphold the highest ethical standards in all our actions.', icon: Shield },
]

const form = ref({
  name: '',
  email: '',
  message: ''
})

const submitForm = () => {
  // Here you would typically send the form data to a server
  console.log('Form submitted:', form.value)
  // Reset form after submission
  form.value = { name: '', email: '', message: '' }
  alert('Thank you for your message. We will get back to you soon!')
}

// Background animation
const particles = ref([])

const createParticles = () => {
  for (let i = 0; i < 50; i++) {
    particles.value.push({
      id: i,
      x: Math.random() * 100,
      y: Math.random() * 100,
      size: Math.random() * 10 + 5,
      duration: Math.random() * 20 + 10
    })
  }
}

onMounted(() => {
  createParticles()
})
</script>

<template>
  <Navigation />
  <div class="min-h-screen bg-gray-50 relative overflow-hidden">
    <!-- Animated background -->
    <div class="absolute inset-0 overflow-hidden">
      <div v-for="particle in particles" :key="particle.id"
        class="absolute rounded-full bg-blue-500 opacity-20"
        :style="{
          width: `${particle.size}px`,
          height: `${particle.size}px`,
          left: `${particle.x}%`,
          top: `${particle.y}%`,
          animation: `float ${particle.duration}s infinite ease-in-out`
        }">
      </div>
    </div>

    <!-- Hero Section with animated gradient -->
    <section class="relative bg-gradient-to-r from-blue-600 to-indigo-700 text-white overflow-hidden">
      <div class="absolute inset-0 bg-gradient-to-r from-blue-600 to-indigo-700 animate-gradient"></div>
      <div class="container mx-auto px-4 py-20 text-center relative z-10">
        <h1 class="text-4xl md:text-5xl font-bold mb-4">About Our Company</h1>
        <p class="text-xl md:text-2xl max-w-3xl mx-auto">
          We're on a mission to revolutionize the industry with innovative solutions and exceptional service.
        </p>
      </div>
    </section>

    <!-- Our Story Section -->
    <section class="py-20 relative z-10">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-8">Our Story</h2>
        <div class="max-w-3xl mx-auto">
          <p class="text-lg mb-4">
            Founded in 2010, our company began with a simple idea: to make technology accessible to everyone.
            What started as a small team working out of a garage has grown into a global organization with
            offices in 15 countries.
          </p>
          <p class="text-lg">
            Through the years, we've remained committed to our core values of innovation, integrity, and
            customer-centricity. These principles have guided us through challenges and successes alike,
            shaping us into the company we are today.
          </p>
        </div>
      </div>
    </section>

    <!-- Our Mission Section -->
    <section class="bg-white bg-opacity-80 py-20 relative z-10">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-8">Our Mission</h2>
        <div class="max-w-3xl mx-auto text-center">
          <p class="text-xl italic">
            "To empower businesses and individuals with cutting-edge technology solutions that drive growth,
            efficiency, and positive change in the world."
          </p>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section class="py-20 relative z-10">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-12">Meet Our Team</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="member in teamMembers" :key="member.id" class="bg-white rounded-lg shadow-md overflow-hidden transition-transform duration-300 ease-in-out transform hover:scale-105">
            <img :src="TeamPhoto" :alt="member.name" class="w-full h-64 object-cover object-center">
            <div class="p-6">
              <h3 class="text-xl font-semibold mb-2">{{ member.name }}</h3>
              <p class="text-gray-600 mb-4">{{ member.position }}</p>
              <p class="text-gray-700">{{ member.bio }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Values Section -->
    <section class="bg-white bg-opacity-80 py-20 relative z-10">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-12">Our Values</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div v-for="value in companyValues" :key="value.id" class="bg-white rounded-lg shadow-md p-6 transition-transform duration-300 ease-in-out transform hover:scale-105">
            <component :is="value.icon" class="w-12 h-12 text-blue-600 mb-4" />
            <h3 class="text-xl font-semibold mb-2">{{ value.title }}</h3>
            <p class="text-gray-700">{{ value.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section class="py-20 relative z-10">
      <div class="container mx-auto px-4">
        <h2 class="text-3xl font-bold text-center mb-8">Get in Touch</h2>
        <div class="max-w-lg mx-auto bg-white bg-opacity-90 rounded-lg shadow-md p-8">
          <form @submit.prevent="submitForm" class="space-y-6">
            <div>
              <label for="name" class="block text-sm font-medium text-gray-700">Name</label>
              <input type="text" id="name" v-model="form.name" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50">
            </div>
            <div>
              <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
              <input type="email" id="email" v-model="form.email" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50">
            </div>
            <div>
              <label for="message" class="block text-sm font-medium text-gray-700">Message</label>
              <textarea id="message" v-model="form.message" rows="4" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring focus:ring-blue-500 focus:ring-opacity-50"></textarea>
            </div>
            <div>
              <button type="submit" class="w-full bg-blue-600 text-white py-2 px-4 rounded-md hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50 transition duration-300 ease-in-out">
                Send Message
              </button>
            </div>
          </form>
        </div>
      </div>
    </section>
  </div>
  <Footer />
</template>

<style scoped>
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.animate-gradient {
  background-size: 200% 200%;
  animation: gradient 15s ease infinite;
}
</style>
