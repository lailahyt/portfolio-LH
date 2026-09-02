<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import projectsData from './data/projects.json'
import ProjectCard from './components/ProjectCard.vue'

const currentLang = ref('id')
const projects = ref(projectsData)

const toggleLanguage = (lang) => {
  currentLang.value = lang
}

const cvPath = computed(() => {
  return currentLang.value === 'en'
    ? '/assets/CV_LailaHayati_Frontend_EN.pdf'
    : '/assets/CV_LailaHayati_Frontend.pdf'
})

// Typing Effect Dynamic Roles
const roles = ["Frontend Web Developer", "Web Application Developer"]
const typingText = ref('')
let roleIndex = 0
let charIndex = 0
let isDeleting = false
let typingTimeout = null

const typeEffect = () => {
  const currentRole = roles[roleIndex]
  
  if (isDeleting) {
    typingText.value = currentRole.substring(0, charIndex - 1)
    charIndex--
  } else {
    typingText.value = currentRole.substring(0, charIndex + 1)
    charIndex++
  }

  let typeSpeed = isDeleting ? 40 : 80

  if (!isDeleting && charIndex === currentRole.length) {
    typeSpeed = 2000
    isDeleting = true
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false
    roleIndex = (roleIndex + 1) % roles.length
    typeSpeed = 500
  }

  typingTimeout = setTimeout(typeEffect, typeSpeed)
}

onMounted(() => {
  typeEffect()
})

onUnmounted(() => {
  if (typingTimeout) clearTimeout(typingTimeout)
})
</script>

<template>
  <div class="min-h-screen bg-[var(--color-bg-main)] text-[var(--color-body-brown)] font-sans">
    <!-- 1. NAVBAR -->
    <nav class="sticky top-0 z-40 bg-[var(--color-bg-main)]/95 backdrop-blur-md border-b border-[var(--color-border-warm)]">
      <div class="max-w-6xl mx-auto px-4 py-3.5 flex justify-between items-center">
        <a href="#" class="text-xl font-bold font-serif text-[var(--color-title-dark)]">LH.</a>
        
        <div class="flex items-center gap-6">
          <div class="hidden md:flex gap-6 text-sm font-medium text-[var(--color-title-dark)]">
            <a href="#overview" class="hover:text-[var(--color-taupe-primary)] transition">{{ currentLang === 'id' ? 'Overview' : 'Overview' }}</a>
            <a href="#services" class="hover:text-[var(--color-taupe-primary)] transition">{{ currentLang === 'id' ? 'Layanan' : 'Services' }}</a>
            <a href="#capabilities" class="hover:text-[var(--color-taupe-primary)] transition">{{ currentLang === 'id' ? 'Kredensial' : 'Credentials' }}</a>
            <a href="#projects" class="hover:text-[var(--color-taupe-primary)] transition">{{ currentLang === 'id' ? 'Proyek' : 'Projects' }}</a>
          </div>

          <!-- Switcher ID / EN Asli -->
          <div class="flex items-center gap-1.5 bg-white/60 px-2.5 py-1 rounded-full border border-black/10 text-xs font-semibold">
            <button 
              @click="toggleLanguage('id')"
              :class="[
                'px-1.5 py-0.5 rounded transition cursor-pointer',
                currentLang === 'id' ? 'bg-white text-[#1a365d] font-bold shadow-xs' : 'text-slate-400 hover:text-slate-700'
              ]"
            >
              ID
            </button>
            <span class="text-slate-300">|</span>
            <button 
              @click="toggleLanguage('en')"
              :class="[
                'px-1.5 py-0.5 rounded transition cursor-pointer',
                currentLang === 'en' ? 'bg-white text-[#1a365d] font-bold shadow-xs' : 'text-slate-400 hover:text-slate-700'
              ]"
            >
              EN
            </button>
          </div>
        </div>
      </div>
    </nav>

    <!-- 2. HERO / OVERVIEW SECTION -->
    <section id="overview" class="py-12 md:py-20">
      <div class="max-w-6xl mx-auto px-4">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-center">
          <div class="lg:col-span-8 space-y-4">
            <h1 class="text-4xl md:text-5xl font-serif text-[var(--color-title-dark)]">Laila Hayati</h1>
            
            <p class="text-lg text-[var(--color-muted-brown)] font-normal">
              <span>{{ currentLang === 'id' ? 'Lulusan Teknik Informatika' : 'Informatics Engineering Graduate' }}</span>
              <span class="mx-2">|</span>
              <span class="font-semibold text-[var(--color-taupe-primary)]">{{ typingText }}</span>
              <span class="animate-pulse text-[var(--color-taupe-primary)]">|</span>
            </p>

            <p class="text-sm md:text-base text-[var(--color-body-brown)] leading-relaxed max-w-xl">
              {{ currentLang === 'id' 
                ? 'Halo! Saya Laila Hayati, lulusan Teknik Informatika Politeknik Negeri Banjarmasin yang berfokus pada Frontend Web Development. Memiliki keahlian dalam merancang antarmuka pengguna (UI/UX) yang intuitif, interaktif, dan responsif menggunakan JavaScript (ES6+), HTML5, CSS3, dan Bootstrap.' 
                : 'Hello! I\'m Laila Hayati, an Informatics Engineering graduate specializing in Frontend Web Development. Experienced in building intuitive, interactive, and fully responsive web user interfaces using JavaScript (ES6+), HTML5, CSS3, and Bootstrap.' 
              }}
            </p>

            <!-- Buttons & Social Links Asli -->
            <div class="pt-4 space-y-4">
              <div class="flex flex-wrap items-center gap-3">
                <a href="mailto:laihyt24@gmail.com" class="bg-[var(--color-taupe-primary)] text-white px-5 py-2.5 rounded-lg text-sm font-medium hover:bg-[var(--color-taupe-hover)] transition flex items-center gap-2">
                  <i class="bi bi-envelope-fill me-2"></i><span>{{ currentLang === 'id' ? 'Email Saya' : 'Email Me' }}</span>
                </a>
                <a :href="cvPath" target="_blank" class="border border-[var(--color-taupe-primary)] text-[var(--color-taupe-primary)] px-5 py-2.5 rounded-lg text-sm font-medium hover:bg-[var(--color-taupe-primary)] hover:text-white transition flex items-center gap-2">
                  <i class="bi bi-file-earmark-person-fill me-2"></i> <span>{{ currentLang === 'id' ? 'Unduh CV' : 'Download CV' }}</span>
                </a>
              </div>
            </div>
          </div>

          <div class="lg:col-span-4 flex justify-center">
            <div class="p-3 bg-white border border-[var(--color-border-warm)] rounded-2xl shadow-sm">
              <img src="/assets/profil.png" alt="Laila Hayati" class="w-64 h-80 object-cover rounded-xl" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. SERVICES SECTION -->
    <section id="services" class="py-16 bg-[var(--color-bg-secondary)]">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-2xl font-serif text-[var(--color-title-dark)] mb-8 pb-3 relative after:content-[''] after:absolute after:bottom-0 after:left-0 after:w-12 after:h-[2px] after:bg-[var(--color-taupe-primary)]">
          {{ currentLang === 'id' ? 'How I Can Help You' : 'How I Can Help You' }}
        </h2>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl shadow-xs hover:-translate-y-1 transition duration-300">
            <div class="text-3xl text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-layout-text-window-reverse"></i></div>
            <h4 class="font-serif font-semibold text-lg text-[var(--color-title-dark)] mb-2">Frontend Web Development</h4>
            <p class="text-sm text-[var(--color-muted-brown)] leading-relaxed">
              {{ currentLang === 'id'
                ? 'Mengubah rancangan antarmuka (Figma/Wireframe) menjadi tampilan website interaktif, bersih, modern, dan responsif di berbagai ukuran layar menggunakan HTML, CSS, JavaScript, dan Bootstrap.'
                : 'Converting design wireframes (Figma) into clean, modern, interactive, and responsive web interfaces across various devices using HTML, CSS, JavaScript, and Bootstrap.'
              }}
            </p>
          </div>

          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl shadow-xs hover:-translate-y-1 transition duration-300">
            <div class="text-3xl text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-code-slash"></i></div>
            <h4 class="font-serif font-semibold text-lg text-[var(--color-title-dark)] mb-2">Web Application Development</h4>
            <p class="text-sm text-[var(--color-muted-brown)] leading-relaxed">
              {{ currentLang === 'id'
                ? 'Membangun aplikasi web fungsional dari nol (from scratch) untuk kebutuhan pemantauan, pengelolaan data (CRUD), hingga Sistem Pendukung Keputusan (DSS) berbasis Laravel atau PHP Native.'
                : 'Building functional web applications from scratch for monitoring, CRUD data management, and Decision Support Systems (DSS) powered by Laravel or Native PHP.'
              }}
            </p>
          </div>

          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl shadow-xs hover:-translate-y-1 transition duration-300">
            <div class="text-3xl text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-diagram-3"></i></div>
            <h4 class="font-serif font-semibold text-lg text-[var(--color-title-dark)] mb-2">Database & System Modeling</h4>
            <p class="text-sm text-[var(--color-muted-brown)] leading-relaxed">
              {{ currentLang === 'id'
                ? 'Merancang skema dan arsitektur data aplikasi secara efisien menggunakan pemodelan relasional (Conceptual, Logical, dan Physical Data Model) serta metodologi terstruktur.'
                : 'Designing efficient database schemas and architectures using relational data modeling (Conceptual, Logical, and Physical Data Models) and structured development methodologies.'
              }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. CAPABILITIES & CREDENTIALS -->
    <section id="capabilities" class="py-16">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-2xl font-serif text-[var(--color-title-dark)] mb-8 pb-3 relative after:content-[''] after:absolute after:bottom-0 after:left-0 after:w-12 after:h-[2px] after:bg-[var(--color-taupe-primary)]">
          {{ currentLang === 'id' ? 'Capabilities & Credentials' : 'Capabilities & Credentials' }}
        </h2>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl">
            <h5 class="text-xs uppercase font-bold tracking-wider text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-code-square me-2"></i>{{ currentLang === 'id' ? 'Languages & Frameworks' : 'Languages & Frameworks' }}</h5>
            <div class="flex flex-wrap gap-1">
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">PHP</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Laravel</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Vue 3</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">JavaScript</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">HTML5</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">CSS3</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Bootstrap</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Tailwind CSS</span>
            </div>
          </div>

          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl">
            <h5 class="text-xs uppercase font-bold tracking-wider text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-tools me-2"></i>{{ currentLang === 'id' ? 'Database & Tools' : 'Database & Tools' }}</h5>
            <div class="flex flex-wrap gap-1">
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">MySQL</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">phpMyAdmin</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">VS Code</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Git & GitHub</span>
            </div>
          </div>

          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl">
            <h5 class="text-xs uppercase font-bold tracking-wider text-[var(--color-taupe-primary)] mb-3"><i class="bi bi-cpu me-2"></i>{{ currentLang === 'id' ? 'Core Competencies' : 'Core Competencies' }}</h5>
            <div class="flex flex-wrap gap-1">
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Frontend Development</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Database Modeling (CDM/LDM/PDM)</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">Waterfall Methodology</span>
              <span class="bg-[var(--color-bg-secondary)] text-[var(--color-title-dark)] border border-[var(--color-border-warm)] px-3 py-1 rounded-md text-xs font-medium">TOPSIS Algorithm</span>
            </div>
          </div>
        </div>

<!-- Grid Baris Bawah: Education & Certificates/Profiles -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <!-- Card 1: Education -->
          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl flex flex-col justify-between shadow-xs">
            <div>
              <h5 class="text-xs font-bold uppercase tracking-wider text-[var(--color-taupe-primary)] mb-3 flex items-center gap-2">
                <i class="bi bi-mortarboard-fill"></i>
                <span>{{ currentLang === 'id' ? 'Pendidikan' : 'Education' }}</span>
              </h5>
              <p class="font-bold text-lg text-[var(--color-title-dark)]">
                {{ currentLang === 'id' ? 'D3 Teknik Informatika' : 'Associate Degree (D3) in Informatics Engineering' }}
              </p>
              <p class="text-sm text-[var(--color-muted-brown)]">
                {{ currentLang === 'id' ? 'Politeknik Negeri Banjarmasin' : 'State Polytechnic of Banjarmasin' }}
              </p>
            </div>
          </div>

          <!-- Card 2: Certificates & External Links -->
          <div class="p-6 bg-white border border-[var(--color-border-warm)] rounded-xl flex flex-col justify-between shadow-xs">
            <div>
              <h5 class="text-xs font-bold uppercase tracking-wider text-[var(--color-taupe-primary)] mb-3 flex items-center gap-2">
                <i class="bi bi-patch-check-fill"></i>
                <span>{{ currentLang === 'id' ? 'Sertifikat & Profil' : 'Certificates & Profiles' }}</span>
              </h5>
              <p class="text-sm text-[var(--color-muted-brown)] mb-4">
                {{ currentLang === 'id' 
                  ? 'Kumpulan sertifikat pelatihan, serta tautan ke profil profesional saya.'
                  : 'Collection of training certificates, and online profile links.'
                }}
              </p>
            </div>

            <!-- 3 Tombol Tautan Tergabung -->
            <div class="flex flex-wrap items-center gap-2 pt-2 border-t border-[var(--color-border-warm)]">
              <!-- Tombol Drive Sertifikat -->
              <a 
                href="https://drive.google.com/drive/folders/17h6QKbg02OGcIoiQ34AJu2n941mkI4Fi?usp=drive_links" 
                target="_blank" 
                class="flex-1 text-center border border-[var(--color-taupe-primary)] text-[var(--color-taupe-primary)] py-2 px-3 rounded-lg text-xs font-semibold hover:bg-[var(--color-taupe-primary)] hover:text-white transition flex items-center justify-center gap-2"
              title="Sertifikat"
              >
                <i class="bi bi-file-earmark-person-fill"></i>
                <span>{{ currentLang === 'id' ? 'Lihat Sertifikat' : 'View Certificates' }}</span>
              </a>

              <!-- Tombol GitHub -->
              <a 
                href="https://github.com/lailahyt" 
                target="_blank" 
                class="border border-[var(--color-taupe-primary)] text-slate-700 bg-slate-50 py-2 px-3 rounded-lg text-xs font-semibold hover:bg-[var(--color-taupe-primary)] hover:text-white transition flex items-center gap-1.5"
                title="GitHub Profile"
              >
                <i class="bi bi-github"></i>
                <span>GitHub</span>
              </a>

              <!-- Tombol LinkedIn -->
              <a 
                href="https://www.linkedin.com/in/laila-hayati-603a3528b/" 
                target="_blank" 
                class="border border-[var(--color-taupe-primary)] text-slate-700 bg-slate-50 py-2 px-3 rounded-lg text-xs font-semibold hover:bg-[var(--color-taupe-primary)] hover:text-white transition flex items-center gap-1.5"
                title="LinkedIn Profile"
              >
                <i class="bi bi-linkedin"></i>
                <span>LinkedIn</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 5. PROJECTS SECTION -->
    <section id="projects" class="py-16 bg-[var(--color-bg-secondary)]">
      <div class="max-w-6xl mx-auto px-4">
        <h2 class="text-2xl font-serif text-[var(--color-title-dark)] mb-8 pb-3 relative after:content-[''] after:absolute after:bottom-0 after:left-0 after:w-12 after:h-[2px] after:bg-[var(--color-taupe-primary)]">
          {{ currentLang === 'id' ? 'Selected Works' : 'Selected Works' }}
        </h2>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <ProjectCard 
            v-for="project in projects" 
            :key="project.id" 
            :project="project"
            :current-lang="currentLang"
          />
        </div>
      </div>
    </section>

    <!-- 6. FOOTER -->
    <footer class="py-6 bg-[var(--color-bg-secondary)] text-center border-t border-[var(--color-border-warm)] text-sm text-[var(--color-muted-brown)]">
      <div class="max-w-6xl mx-auto px-4">
        <p>© 2026 Laila Hayati. {{ currentLang === 'id' ? 'Built with Vue 3 & Tailwind CSS.' : 'Built with Vue 3 & Tailwind CSS.' }}</p>
      </div>
    </footer>
  </div>
</template>