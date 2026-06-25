<script setup lang="ts">
import { ref, onMounted } from 'vue'

const visible = ref(false)
onMounted(() => { visible.value = true })
</script>

<template>
  <section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden bg-grid bg-radial">
    <!-- Animated background orbs -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none">
      <div class="absolute -top-40 -left-40 w-80 h-80 bg-violet-600/20 rounded-full blur-[120px] animate-float" />
      <div class="absolute top-1/2 -right-40 w-96 h-96 bg-indigo-600/15 rounded-full blur-[120px] animate-float" style="animation-delay: -2s" />
      <div class="absolute -bottom-20 left-1/3 w-72 h-72 bg-blue-600/10 rounded-full blur-[100px] animate-float" style="animation-delay: -4s" />
    </div>

    <div class="relative z-10 max-w-4xl mx-auto px-6 text-center">
      <!-- Badge -->
      <div :class="['inline-flex items-center gap-2 px-4 py-2 rounded-full glass text-sm text-zinc-400 mb-8 transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <span class="relative flex h-2 w-2">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75" />
          <span class="relative inline-flex rounded-full h-2 w-2 bg-green-500" />
        </span>
        Open to AI Internship Opportunities
      </div>

      <!-- Name -->
      <h1 :class="['text-5xl md:text-7xl lg:text-8xl font-black tracking-tight mb-6 transition-all duration-700 delay-100', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <span class="text-white">刘</span><span class="text-white">振</span><span class="text-gradient">源</span>
      </h1>

      <!-- Subtitle -->
      <p :class="['text-lg md:text-xl text-zinc-400 max-w-2xl mx-auto mb-10 leading-relaxed transition-all duration-700 delay-200', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <span class="block text-2xl md:text-3xl font-light text-white mb-2">AI 驱动开发 &middot; 全栈探索者</span>
        广西民族大学 · 软件工程 · 2027届<br />
        以 AI 工具赋能开发，追求工程效率与代码质量
      </p>

      <!-- CTA buttons -->
      <div :class="['flex flex-wrap justify-center gap-4 transition-all duration-700 delay-300', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <a
          href="#projects"
          class="inline-flex items-center gap-2 px-8 py-3.5 rounded-xl text-sm font-semibold text-white bg-gradient-to-r from-violet-600 to-indigo-600 hover:from-violet-500 hover:to-indigo-500 transition-all duration-300 shadow-lg shadow-violet-600/20 hover:shadow-violet-600/40"
        >
          查看证书
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
          </svg>
        </a>
        <a
          href="#contact"
          class="inline-flex items-center gap-2 px-8 py-3.5 rounded-xl text-sm font-semibold text-zinc-300 glass hover:text-white hover:border-zinc-600 border border-zinc-700/50 transition-all duration-300"
        >
          联系我
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
          </svg>
        </a>
      </div>

      <!-- Stats -->
      <div :class="['flex flex-wrap justify-center gap-8 md:gap-16 mt-16 transition-all duration-700 delay-500', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <div class="text-center">
          <div class="text-3xl font-bold text-white">2+</div>
          <div class="text-xs text-zinc-500 mt-1">AI 项目经历</div>
        </div>
        <div class="text-center">
          <div class="text-3xl font-bold text-white">5+</div>
          <div class="text-xs text-zinc-500 mt-1">掌握技术栈</div>
        </div>
        <div class="text-center">
          <div class="text-3xl font-bold text-white">2027</div>
          <div class="text-xs text-zinc-500 mt-1">毕业年份</div>
        </div>
      </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 animate-bounce">
      <svg class="w-6 h-6 text-zinc-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
      </svg>
    </div>
  </section>
</template>
