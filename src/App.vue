<script setup lang="ts">
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import NavBar from './components/NavBar.vue'
</script>

<template>
  <div class="relative min-h-screen bg-[#0a0a0f] text-zinc-200 overflow-hidden">
    <NavBar />
    <main>
      <HeroSection />
      <AboutSection />
      <SkillsSection />
      <ExperienceSection />
      <ProjectsSection />
      <ContactSection />
    </main>
    <footer class="py-8 text-center text-sm text-zinc-600 border-t border-zinc-800/50 bg-[#0a0a0f]">
      <p>&copy; 2026 刘振源. Designed & Built with Vue 3 &amp; Tailwind CSS.</p>
    </footer>
  </div>
</template>
