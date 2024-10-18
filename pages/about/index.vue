<template>
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
          <NuxtLink to="./about" class="border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700 inline-flex items-center px-1 pt-1 border-b-2 text-sm font-medium">About</NuxtLink>
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


  <div class="min-h-screen">
    <main class="max-w-7xl mx-auto sm:px-6 lg:px-8">
      <div class="px-4 py-6 sm:px-0">
        <div class="overflow-hidden">
          <div class="p-6">
            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Our Mission
              </h2>
              <p class="text-gray-700 mb-4 leading-relaxed">
                At CompanyInsider, our mission is to empower job seekers and
                employees by providing a platform for honest, transparent
                company reviews. We believe that by fostering an environment of
                open communication, we can help create better workplaces and
                assist individuals in making informed career decisions.
              </p>
              <p class="text-gray-700 leading-relaxed">
                Our goal is to bridge the information gap between companies and
                potential employees, ensuring that everyone has access to real
                insights about company culture, work environment, and growth
                opportunities.
              </p>
            </section>

            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                How It Works
              </h2>
              <ol class="list-decimal list-inside text-gray-700 space-y-2">
                <li
                  v-for="(step, index) in howItWorks"
                  :key="index"
                  class="p-2 rounded transition-all duration-300 ease-in-out transform hover:scale-105 hover:bg-indigo-100"
                >
                  {{ step }}
                </li>
              </ol>
            </section>

            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Our Values
              </h2>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div
                  v-for="(value, index) in companyValues"
                  :key="index"
                  class="bg-gray-50 p-4 rounded-lg transition-all duration-300 ease-in-out transform hover:scale-105 hover:shadow-lg"
                  @mouseenter="highlightValue(index)"
                  @mouseleave="unhighlightValue(index)"
                >
                  <h3 class="text-lg font-medium text-indigo-900 mb-2">
                    {{ value.title }}
                  </h3>
                  <p
                    class="text-gray-700"
                    :class="{ 'font-bold': value.highlighted }"
                  >
                    {{ value.description }}
                  </p>
                </div>
              </div>
            </section>

            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Our Team
              </h2>
              <p class="text-gray-700 mb-4 leading-relaxed">
                CompanyInsider was founded by a diverse group of professionals
                who recognized the need for greater transparency in the job
                market. Our team consists of experienced developers, data
                scientists, and industry experts who are passionate about
                creating a platform that makes a difference in people's careers.
              </p>
              <div
                class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6 mt-8"
              >
                <div
                  v-for="member in teamMembers"
                  :key="member.name"
                  class="bg-white shadow-md rounded-lg overflow-hidden transition-all duration-300 ease-in-out transform hover:scale-105 hover:shadow-xl"
                >
                  <img
                    src="../../assets/images/team_photo.jpg"
                    :alt="member.name"
                    class="w-full h-48 object-cover"
                  />
                  <div class="p-4">
                    <h3 class="text-lg font-medium text-indigo-900">
                      {{ member.name }}
                    </h3>
                    <p class="text-sm text-gray-600">{{ member.role }}</p>
                  </div>
                </div>
              </div>
            </section>

            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Our Commitment to Privacy
              </h2>
              <p class="text-gray-700 mb-4 leading-relaxed">
                We understand the sensitive nature of workplace reviews and take
                your privacy seriously. CompanyInsider is committed to
                protecting the anonymity of our users and ensuring that your
                personal information remains confidential.
              </p>
              <ul class="list-disc list-inside text-gray-700 space-y-2">
                <li
                  v-for="(commitment, index) in privacyCommitments"
                  :key="index"
                  class="p-2 rounded transition-all duration-300 ease-in-out transform hover:scale-105 hover:bg-indigo-100"
                >
                  {{ commitment }}
                </li>
              </ul>
            </section>

            <section class="mb-12 fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Join Our Community
              </h2>
              <p class="text-gray-700 mb-4 leading-relaxed">
                Become a part of the CompanyInsider community today and help
                shape the future of work. Whether you're looking for your next
                career move or want to share your experiences to help others,
                your voice matters.
              </p>
              <div class="mt-6">
                <a
                  href="#"
                  class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-300 ease-in-out transform hover:scale-105"
                >
                  Sign Up Now
                </a>
              </div>
            </section>

            <section class="fade-in-element">
              <h2 class="text-2xl font-semibold text-indigo-900 mb-4">
                Contact Us
              </h2>
              <p class="text-gray-700 mb-4 leading-relaxed">
                Have questions, suggestions, or feedback? We'd love to hear from
                you! Reach out to our support team at support@companyinsider.com
                or use the contact form below.
              </p>
              <form
                @submit.prevent="submitContactForm"
                class="grid grid-cols-1 gap-6"
              >
                <div>
                  <label
                    for="name"
                    class="block text-sm font-medium text-gray-700"
                    >Name</label
                  >
                  <input
                    type="text"
                    name="name"
                    id="name"
                    v-model="contactForm.name"
                    class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md bg-white text-gray-900"
                  />
                </div>
                <div>
                  <label
                    for="email"
                    class="block text-sm font-medium text-gray-700"
                    >Email</label
                  >
                  <input
                    type="email"
                    name="email"
                    id="email"
                    v-model="contactForm.email"
                    class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md bg-white text-gray-900"
                  />
                </div>
                <div>
                  <label
                    for="message"
                    class="block text-sm font-medium text-gray-700"
                    >Message</label
                  >
                  <textarea
                    id="message"
                    name="message"
                    rows="4"
                    v-model="contactForm.message"
                    class="mt-1 focus:ring-indigo-500 focus:border-indigo-500 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md bg-white text-gray-900"
                  ></textarea>
                </div>
                <div>
                  <button
                    type="submit"
                    class="inline-flex items-center px-4 py-2 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-300 ease-in-out transform hover:scale-105"
                  >
                    Send Message
                  </button>
                </div>
              </form>
            </section>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const howItWorks = [
  "Create an account or log in to your existing profile.",
  "Search for a company or browse our extensive database.",
  "Read reviews from current and former employees.",
  "Share your own experience by writing a review.",
  "Rate companies based on various factors like work-life balance, culture, and career growth.",
  "Engage with the community by voting on helpful reviews.",
];

const companyValues = ref([
  {
    title: "Transparency",
    description:
      "We believe in open and honest communication, both on our platform and within our organization.",
    highlighted: false,
  },
  {
    title: "Empowerment",
    description:
      "We aim to give individuals the tools and information they need to make informed career decisions.",
    highlighted: false,
  },
  {
    title: "Innovation",
    description:
      "We constantly strive to improve our platform and bring new ideas to the job market.",
    highlighted: false,
  },
  {
    title: "Integrity",
    description:
      "We maintain high ethical standards and ensure the authenticity of the reviews on our platform.",
    highlighted: false,
  },
]);

const highlightValue = (index) => {
  companyValues.value[index].highlighted = true;
};

const unhighlightValue = (index) => {
  companyValues.value[index].highlighted = false;
};

const teamMembers = [
  {
    name: "Yaasir Cheekoory",
    role: "CEO & Co-founder",
    avatar: "/placeholder.svg?height=200&width=200",
  },
  {
    name: "Yaasir Cheekoory",
    role: "CTO",
    avatar: "/placeholder.svg?height=200&width=200",
  },
  {
    name: "Yaasir Cheekoory",
    role: "Head of User Experience",
    avatar: "/placeholder.svg?height=200&width=200",
  },
];

const privacyCommitments = [
  "All reviews are posted anonymously by default.",
  "We use advanced encryption to protect your data.",
  "We never share personal information with the companies being reviewed.",
  "Users have full control over their account information and can delete their data at any time.",
];

const contactForm = ref({
  name: "",
  email: "",
  message: "",
});

const submitContactForm = () => {
  console.log("Form submitted:", contactForm.value);
  contactForm.value = { name: "", email: "", message: "" };
  alert("Thank you for your message. We will get back to you soon!");
};

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("fade-in-element");
        }
      });
    },
    { threshold: 0.1 }
  );

  document.querySelectorAll("section").forEach((section) => {
    observer.observe(section);
  });
});
</script>

<style>
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-element {
  animation: fadeIn 1s ease-out forwards;
}

section {
  opacity: 0;
}
</style>
