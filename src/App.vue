<template>
  <div class="bg-slate-950 text-slate-100">
    <!-- Navigation -->
    <nav class="fixed top-0 left-0 right-0 z-50 bg-slate-950/80 backdrop-blur-md border-b border-slate-800">
      <div class="max-w-6xl mx-auto px-4 sm:px-6 py-3 sm:py-4 flex justify-between items-center">
        <div class="text-lg sm:text-xl font-bold gradient-text truncate">{{ data.name }}</div>
        <!-- Desktop Menu -->
        <div class="hidden sm:flex gap-8 items-center">
          <a href="#about" class="text-slate-400 hover:text-slate-100 transition text-sm">О себе</a>
          <a href="#skills" class="text-slate-400 hover:text-slate-100 transition text-sm">Навыки</a>
          <a href="#experience" class="text-slate-400 hover:text-slate-100 transition text-sm">Опыт</a>
          <a href="#contact" class="px-6 py-2 contact-btn text-white rounded-lg text-sm">Связь</a>
        </div>
        <!-- Mobile Menu Button -->
        <button @click="mobileMenuOpen = !mobileMenuOpen" class="sm:hidden text-slate-400 hover:text-slate-100">
          <i :class="mobileMenuOpen ? 'fas fa-times' : 'fas fa-bars'"></i>
        </button>
      </div>
      <!-- Mobile Menu -->
      <div v-if="mobileMenuOpen" class="sm:hidden bg-slate-900/95 border-t border-slate-800 px-4 py-4 space-y-3">
        <a href="#about" class="block text-slate-400 hover:text-slate-100 transition text-sm py-2" @click="mobileMenuOpen = false">О себе</a>
        <a href="#skills" class="block text-slate-400 hover:text-slate-100 transition text-sm py-2" @click="mobileMenuOpen = false">Навыки</a>
        <a href="#experience" class="block text-slate-400 hover:text-slate-100 transition text-sm py-2" @click="mobileMenuOpen = false">Опыт</a>
        <a href="#contact" class="block px-4 py-2 contact-btn text-white rounded-lg text-sm text-center" @click="mobileMenuOpen = false">Связь</a>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero-bg text-white pt-24 sm:pt-32 pb-12 sm:pb-20 relative">
      <div class="max-w-6xl mx-auto px-4 sm:px-6">
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-8 sm:gap-12 items-center">
          <div>
            <div class="inline-block mb-4 sm:mb-6 px-3 py-1.5 sm:px-4 sm:py-2 bg-slate-800 rounded-full text-xs sm:text-sm text-slate-300 border border-slate-700">
              <i class="fas fa-code mr-2"></i> {{ data.title }}
            </div>
            <h1 class="text-3xl sm:text-5xl lg:text-6xl font-bold mb-4 sm:mb-6 leading-tight">
              Привет, я <span class="gradient-text">{{ data.name }}</span>
            </h1>
            <p class="text-base sm:text-lg lg:text-xl text-slate-400 mb-6 sm:mb-8 leading-relaxed">
              {{ data.description }}
            </p>
            <div class="flex flex-col sm:flex-row gap-3 sm:gap-4">
              <a href="#contact" class="px-6 sm:px-8 py-3 sm:py-4 contact-btn text-white rounded-lg flex items-center justify-center sm:justify-start gap-2 text-sm sm:text-base">
                <i class="fas fa-envelope"></i> <span>Получить предложение</span>
              </a>
              <a href="https://github.com/LiC3MeR" target="_blank" class="px-6 sm:px-8 py-3 sm:py-4 bg-slate-800 text-white rounded-lg hover:bg-slate-700 transition flex items-center justify-center gap-2 text-sm sm:text-base">
                <i class="fab fa-github"></i> <span>GitHub</span>
              </a>
            </div>
          </div>
          <div class="flex justify-center mt-8 sm:mt-0">
            <div class="photo-frame floating" :style="{ width: screenWidth < 640 ? '200px' : '300px', height: screenWidth < 640 ? '280px' : '400px' }">
              <img :src="data.photoUrl" :alt="data.name">
            </div>
          </div>
        </div>
        <div class="text-center mt-12 sm:mt-20 scroll-indicator hidden sm:block">
          <i class="fas fa-chevron-down text-slate-500 text-2xl"></i>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-12 sm:py-20 bg-slate-900/50">
      <div class="max-w-6xl mx-auto px-4 sm:px-6">
        <h2 class="text-2xl sm:text-4xl font-bold mb-8 sm:mb-12 gradient-text">О себе</h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 sm:gap-8">
          <div v-for="item in data.about" :key="item.id" class="card-hover p-6 sm:p-8 bg-slate-800/30 rounded-xl">
            <i :class="`fas ${item.icon} text-2xl sm:text-3xl mb-4`" :style="`color: ${getColorClass(item.color)}`"></i>
            <h3 class="text-lg sm:text-xl font-bold mb-3 sm:mb-4">{{ item.title }}</h3>
            <p class="text-slate-400 text-sm sm:text-base">{{ item.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="py-12 sm:py-20">
      <div class="max-w-6xl mx-auto px-4 sm:px-6">
        <h2 class="text-2xl sm:text-4xl font-bold mb-8 sm:mb-12 gradient-text">Навыки</h2>
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 sm:gap-12">
          <div>
            <h3 class="text-lg sm:text-2xl font-bold mb-6 text-white">Backend</h3>
            <div class="space-y-4">
              <div v-for="skill in data.skills.backend" :key="skill.name">
                <div class="flex justify-between mb-2 text-sm sm:text-base">
                  <span class="font-semibold">{{ skill.name }}</span>
                  <span class="text-purple-400">{{ skill.percentage }}%</span>
                </div>
                <div class="h-2 bg-slate-700 rounded-full overflow-hidden">
                  <div class="h-full bg-gradient-to-r from-purple-500 to-pink-500" :style="{ width: skill.percentage + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
          <div>
            <h3 class="text-lg sm:text-2xl font-bold mb-6 text-white">Области экспертизы</h3>
            <div class="flex flex-wrap gap-2 sm:gap-3">
              <span v-for="expertise in data.skills.expertise" :key="expertise" class="skill-tag text-xs sm:text-sm">
                {{ expertise }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="py-12 sm:py-20 bg-slate-900/50">
      <div class="max-w-6xl mx-auto px-4 sm:px-6">
        <h2 class="text-2xl sm:text-4xl font-bold mb-8 sm:mb-12 gradient-text">Опыт работы</h2>
        <div class="space-y-6 sm:space-y-8">
          <div v-for="job in data.experience" :key="job.id" class="card-hover p-6 sm:p-8 bg-slate-800/30 rounded-xl" :style="`border-left: 4px solid ${getBorderColor(job.color)}`">
            <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-4 mb-4">
              <div class="flex-1">
                <h3 class="text-xl sm:text-2xl font-bold text-white">{{ job.position }}</h3>
                <p :style="`color: ${getColorClass(job.color)}`" class="font-semibold text-sm sm:text-base">{{ job.company }}</p>
              </div>
              <span :style="`background-color: ${getBackgroundColor(job.color)}`" class="px-3 sm:px-4 py-1.5 sm:py-2 text-xs sm:text-sm font-semibold rounded-full whitespace-nowrap">
                {{ job.startDate }} - {{ job.endDate }}
              </span>
            </div>
            <p class="text-slate-400 mb-3 sm:mb-4 text-sm sm:text-base">{{ job.location }} · Работа в офисе</p>
            <p class="text-slate-300 text-sm sm:text-base">{{ job.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-12 sm:py-20">
      <div class="max-w-4xl mx-auto px-4 sm:px-6">
        <h2 class="text-2xl sm:text-4xl font-bold mb-8 sm:mb-12 text-center gradient-text">Давайте работать вместе</h2>
        <div class="grid grid-cols-2 lg:grid-cols-4 gap-3 sm:gap-6 mb-8 sm:mb-12">
          <a v-for="contact in data.contacts" :key="contact.id" :href="contact.href" target="_blank" class="card-hover p-4 sm:p-6 bg-slate-800/30 rounded-xl text-center hover:text-purple-400 transition">
            <i :class="contact.icon" class="text-2xl sm:text-3xl mb-2 sm:mb-4 block text-purple-400"></i>
            <p class="text-xs sm:text-sm text-slate-400">{{ contact.label }}</p>
            <p class="font-semibold text-white text-xs sm:text-sm truncate">{{ contact.value }}</p>
          </a>
        </div>
        <div class="text-center">
          <a href="mailto:jenzw54@gmail.com?subject=Предложение работы" class="contact-btn px-8 sm:px-10 py-3 sm:py-4 text-white rounded-lg inline-block text-sm sm:text-base">
            <i class="fas fa-paper-plane mr-2"></i> Отправить предложение
          </a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900/50 border-t border-slate-800 py-6 sm:py-8">
      <div class="max-w-6xl mx-auto px-4 sm:px-6 text-center text-slate-500 text-xs sm:text-sm">
        <p>© 2025 {{ data.name }}. {{ data.title }}. Taldykorgan, Kazakhstan</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import data from './data.json'

const mobileMenuOpen = ref(false)
const screenWidth = ref(typeof globalThis !== 'undefined' ? globalThis.innerWidth : 640)

const colorMap = {
  purple: '#a78bfa',
  blue: '#60a5fa',
  green: '#4ade80'
}

const getColorClass = (color) => {
  return colorMap[color] || '#667eea'
}

const getBorderColor = (color) => {
  const colors = {
    purple: 'rgb(168, 85, 247)',
    blue: 'rgb(59, 130, 246)',
    green: 'rgb(34, 197, 94)'
  }
  return colors[color] || 'rgb(102, 126, 234)'
}

const getBackgroundColor = (color) => {
  const colors = {
    purple: 'rgba(168, 85, 247, 0.2)',
    blue: 'rgba(59, 130, 246, 0.2)',
    green: 'rgba(34, 197, 94, 0.2)'
  }
  return colors[color] || 'rgba(102, 126, 234, 0.2)'
}

onMounted(() => {
  // Smooth scroll
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
      e.preventDefault();
      const target = document.querySelector(this.getAttribute('href'));
      if (target) {
        target.scrollIntoView({
          behavior: 'smooth',
          block: 'start'
        });
      }
    });
  });

  // Window resize listener
  const handleResize = () => {
    screenWidth.value = globalThis.innerWidth
  }
  
  globalThis.addEventListener('resize', handleResize)
  
  onBeforeUnmount(() => {
    globalThis.removeEventListener('resize', handleResize)
  })
})
</script>

<style scoped>
</style>
