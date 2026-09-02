<script setup>
// Proyek menerima prop 'project' dan 'currentLang' dari parent component
defineProps({
  project: {
    type: Object,
    required: true
  },
  currentLang: {
    type: String,
    default: 'id'
  }
})
</script>

<template>
  <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden flex flex-col hover:shadow-lg transition duration-300">
    <!-- Gambar Screenshot Proyek -->
    <div class="relative h-48 w-full bg-slate-100 overflow-hidden border-b border-slate-100">
      <img 
        :src="project.image" 
        :alt="project.title" 
        class="w-full h-full object-cover object-top hover:scale-105 transition duration-500"
      />
      <span class="absolute top-3 left-3 bg-slate-900/80 backdrop-blur-xs text-white text-[10px] font-semibold px-2.5 py-1 rounded-full">
        {{ project.category }}
      </span>
    </div>

    <!-- Content Detail Proyek -->
    <div class="p-5 flex-1 flex flex-col justify-between">
      <div>
        <!-- Tech Stack Badges -->
        <div class="flex flex-wrap gap-1.5 mb-3">
          <span 
            v-for="(tech, index) in project.techStack" 
            :key="index"
            class="bg-indigo-50 text-indigo-600 border border-indigo-100 text-[11px] font-semibold px-2 py-0.5 rounded-md"
          >
            {{ tech }}
          </span>
        </div>

        <!-- Judul & Klien -->
        <h3 class="font-bold text-slate-800 text-base mb-1 line-clamp-2">
          {{ project.title }}
        </h3>
        <p class="text-xs font-semibold text-slate-400 mb-3">
          🏢 {{ project.client[currentLang] }}
        </p>

        <!-- Deskripsi Dinamis Sesuai Bahasa (ID/EN) -->
        <p class="text-xs text-slate-600 leading-relaxed mb-4">
          {{ project.description[currentLang] }}
        </p>
      </div>

      <!-- Footer Action Links (GitHub & Live Demo) -->
      <div class="pt-3 border-t border-slate-100 flex items-center gap-2 mt-auto">
        <a 
          v-if="project.githubUrl"
          :href="project.githubUrl" 
          target="_blank"
          class="flex-1 text-center bg-slate-100 text-slate-700 hover:bg-slate-200 py-2 rounded-xl text-xs font-semibold transition flex items-center justify-center gap-1.5"
        >
          <span>💻</span> GitHub
        </a>
        
        <a 
          v-if="project.demoUrl"
          :href="project.demoUrl" 
          target="_blank"
          class="flex-1 text-center bg-indigo-600 text-white hover:bg-indigo-700 py-2 rounded-xl text-xs font-semibold transition flex items-center justify-center gap-1.5 shadow-sm shadow-indigo-200"
        >
          <span>🚀</span> Live Demo
        </a>
      </div>
    </div>
  </div>
</template>