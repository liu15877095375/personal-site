<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const mobileMenuOpen = ref(false)

function onScroll() {
  scrolled.value = window.scrollY > 50
}

onMounted(() => window.addEventListener('scroll', onScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', onScroll))

const navItems = [
  { label: '关于', href: '#about' },
  { label: '技能', href: '#skills' },
  { label: '经历', href: '#experience' },
  { label: '证书', href: '#projects' },
  { label: '联系', href: '#contact' },
]

function scrollTo(href: string) {
  mobileMenuOpen.value = false
  document.querySelector(href)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <nav
    :class="scrolled
      ? 'bg-[#0a0a0f]/80 backdrop-blur-xl border-b border-zinc-800/50'
      : 'bg-transparent border-transparent'"
    class="fixed top-0 inset-x-0 z-50 transition-all duration-500"
  >
    <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
      <a href="#" class="text-xl font-bold text-white tracking-tight" @click.prevent="scrollTo('#hero')">
        <span class="text-gradient">LZY</span>
      </a>

      <!-- Desktop nav -->
      <div class="hidden md:flex items-center gap-8">
        <a
          v-for="item in navItems" :key="item.href"
          :href="item.href"
          class="text-sm text-zinc-400 hover:text-white transition-colors duration-300 tracking-wide"
          @click.prevent="scrollTo(item.href)"
        >{{ item.label }}</a>
      </div>

      <!-- Mobile menu button -->
      <button
        class="md:hidden text-zinc-400 hover:text-white transition-colors p-2"
        @click="mobileMenuOpen = !mobileMenuOpen"
      >
        <svg v-if="!mobileMenuOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <!-- Mobile menu -->
    <Transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-4"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-4"
    >
      <div v-if="mobileMenuOpen" class="md:hidden bg-[#0a0a0f]/95 backdrop-blur-xl border-b border-zinc-800/50 px-6 py-4">
        <a
          v-for="item in navItems" :key="item.href"
          :href="item.href"
          class="block py-3 text-sm text-zinc-400 hover:text-white transition-colors duration-300 tracking-wide"
          @click.prevent="scrollTo(item.href)"
        >{{ item.label }}</a>
      </div>
    </Transition>
  </nav>
</template>
