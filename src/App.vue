<template>
  <div class="bg-slate-950 text-slate-100">
    <!-- Navigation -->
    <nav class="fixed top-0 left-0 right-0 z-50 bg-slate-950/80 backdrop-blur-md border-b border-slate-800">
      <div class="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
        <div class="text-xl font-bold gradient-text">{{ data.name }}</div>
        <div class="flex gap-8 items-center">
          <a href="#about" class="text-slate-400 hover:text-slate-100 transition">О себе</a>
          <a href="#skills" class="text-slate-400 hover:text-slate-100 transition">Навыки</a>
          <a href="#experience" class="text-slate-400 hover:text-slate-100 transition">Опыт</a>
          <a href="#contact" class="px-6 py-2 contact-btn text-white rounded-lg">Связь</a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero-bg text-white pt-32 pb-20 relative">
      <div class="max-w-6xl mx-auto px-6">
        <div class="grid grid-cols-2 gap-12 items-center">
          <div>
            <div class="inline-block mb-6 px-4 py-2 bg-slate-800 rounded-full text-sm text-slate-300 border border-slate-700">
              <i class="fas fa-code mr-2"></i> {{ data.title }}
            </div>
            <h1 class="text-6xl font-bold mb-6 leading-tight">
              Привет, я <span class="gradient-text">{{ data.name }}</span>
            </h1>
            <p class="text-xl text-slate-400 mb-8 leading-relaxed">
              {{ data.description }}
            </p>
            <div class="flex gap-4">
              <a href="#contact" class="px-8 py-4 contact-btn text-white rounded-lg flex items-center gap-2">
                <i class="fas fa-envelope"></i> Получить предложение
              </a>
              <a href="https://github.com/LiC3MeR" target="_blank" class="px-8 py-4 bg-slate-800 text-white rounded-lg hover:bg-slate-700 transition flex items-center gap-2">
                <i class="fab fa-github"></i> GitHub
              </a>
            </div>
          </div>
          <div class="flex justify-center">
            <div class="photo-frame floating">
              <img :src="data.photoUrl" :alt="data.name">
            </div>
          </div>
        </div>
        <div class="text-center mt-20 scroll-indicator">
          <i class="fas fa-chevron-down text-slate-500 text-2xl"></i>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-20 bg-slate-900/50">
      <div class="max-w-6xl mx-auto px-6">
        <h2 class="text-4xl font-bold mb-12 gradient-text">О себе</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="item in data.about" :key="item.id" class="card-hover p-8 bg-slate-800/30 rounded-xl">
            <i :class="`fas ${item.icon} text-3xl mb-4`" :style="`color: ${getColorClass(item.color)}`"></i>
            <h3 class="text-xl font-bold mb-4">{{ item.title }}</h3>
            <p class="text-slate-400">{{ item.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="py-20">
      <div class="max-w-6xl mx-auto px-6">
        <h2 class="text-4xl font-bold mb-12 gradient-text">Навыки</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
          <div>
            <h3 class="text-2xl font-bold mb-6 text-white">Backend</h3>
            <div class="space-y-4">
              <div v-for="skill in data.skills.backend" :key="skill.name">
                <div class="flex justify-between mb-2">
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
            <h3 class="text-2xl font-bold mb-6 text-white">Области экспертизы</h3>
            <div class="flex flex-wrap gap-3">
              <span v-for="expertise in data.skills.expertise" :key="expertise" class="skill-tag">
                {{ expertise }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="py-20 bg-slate-900/50">
      <div class="max-w-6xl mx-auto px-6">
        <h2 class="text-4xl font-bold mb-12 gradient-text">Опыт работы</h2>
        <div class="space-y-8">
          <div v-for="job in data.experience" :key="job.id" class="card-hover p-8 bg-slate-800/30 rounded-xl" :style="`border-left: 4px solid ${getBorderColor(job.color)}`">
            <div class="flex items-start justify-between mb-4">
              <div>
                <h3 class="text-2xl font-bold text-white">{{ job.position }}</h3>
                <p :style="`color: ${getColorClass(job.color)}`" class="font-semibold">{{ job.company }}</p>
              </div>
              <span :style="`background-color: ${getBackgroundColor(job.color)}`" class="px-4 py-2 text-sm font-semibold rounded-full">
                {{ job.startDate }} - {{ job.endDate }}
              </span>
            </div>
            <p class="text-slate-400 mb-4">{{ job.location }} · Работа в офисе</p>
            <p class="text-slate-300">{{ job.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-20">
      <div class="max-w-4xl mx-auto px-6">
        <h2 class="text-4xl font-bold mb-12 text-center gradient-text">Давайте работать вместе</h2>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6 mb-12">
          <a v-for="contact in data.contacts" :key="contact.id" :href="contact.href" target="_blank" class="card-hover p-6 bg-slate-800/30 rounded-xl text-center hover:text-purple-400 transition">
            <i :class="contact.icon" class="text-3xl mb-4 block text-purple-400"></i>
            <p class="text-sm text-slate-400">{{ contact.label }}</p>
            <p class="font-semibold text-white text-sm truncate">{{ contact.value }}</p>
          </a>
        </div>
        <div class="text-center">
          <a href="mailto:jenzw54@gmail.com?subject=Предложение работы" class="contact-btn px-10 py-4 text-white rounded-lg inline-block">
            <i class="fas fa-paper-plane mr-2"></i> Отправить предложение
          </a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900/50 border-t border-slate-800 py-8">
      <div class="max-w-6xl mx-auto px-6 text-center text-slate-500">
        <p>© 2025 {{ data.name }}. {{ data.title }}. Taldykorgan, Kazakhstan</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import data from './data.json'

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
})
</script>

<style scoped>
</style>
