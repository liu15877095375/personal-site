<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

const section = ref<HTMLElement | null>(null)
const visible = ref(false)

onMounted(() => {
  if (section.value) {
    const { stop } = useIntersectionObserver(section, ([{ isIntersecting }]) => {
      if (isIntersecting) {
        visible.value = true
        stop()
      }
    }, { threshold: 0.2 })
  }
})
</script>

<template>
  <section id="about" ref="section" class="py-24 md:py-32 px-6">
    <div class="max-w-4xl mx-auto">
      <div :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <p class="text-sm font-medium text-violet-400 tracking-widest uppercase mb-4">About</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-12">
          关于我
        </h2>
      </div>

      <div class="grid md:grid-cols-2 gap-12">
        <!-- Left: Education -->
        <div :class="['transition-all duration-700 delay-150', visible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-8']">
          <h3 class="text-lg font-semibold text-white mb-6 flex items-center gap-3">
            <span class="w-8 h-8 rounded-lg bg-violet-600/20 flex items-center justify-center">
              <svg class="w-4 h-4 text-violet-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 14l9-5-9-5-9 5 9 5z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 14l9-5-9-5-9 5 9 5z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 14v7" />
              </svg>
            </span>
            教育背景
          </h3>
          <div class="glass rounded-2xl p-6 space-y-4">
            <div>
              <p class="text-white font-semibold">广西民族大学</p>
              <p class="text-sm text-zinc-400">软件工程 · 本科</p>
              <p class="text-sm text-zinc-500">2023.09 - 2027.06</p>
            </div>
            <div class="border-t border-zinc-800 pt-4 space-y-2">
              <p class="text-sm text-zinc-300 flex items-start gap-2">
                <span class="text-violet-400 mt-0.5">&#9679;</span>
                学习数据结构、计算机组成原理等课程
              </p>
              <p class="text-sm text-zinc-300 flex items-start gap-2">
                <span class="text-violet-400 mt-0.5">&#9679;</span>
                类ICPC竞赛经验，蓝桥杯竞赛经验
              </p>
              <p class="text-sm text-zinc-300 flex items-start gap-2">
                <span class="text-violet-400 mt-0.5">&#9679;</span>
                CET-4
              </p>
              <p class="text-sm text-zinc-300 flex items-start gap-2">
                <span class="text-violet-400 mt-0.5">&#9679;</span>
                文秘工作经历、辩论赛经历
              </p>
            </div>
          </div>
        </div>

        <!-- Right: Focus -->
        <div :class="['transition-all duration-700 delay-300', visible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-8']">
          <h3 class="text-lg font-semibold text-white mb-6 flex items-center gap-3">
            <span class="w-8 h-8 rounded-lg bg-blue-600/20 flex items-center justify-center">
              <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
              </svg>
            </span>
            当前方向
          </h3>
          <div class="glass rounded-2xl p-6 space-y-4">
            <div class="flex items-start gap-3">
              <span class="text-xl">&#129302;</span>
              <div>
                <p class="text-white font-semibold">AI 驱动开发</p>
                <p class="text-sm text-zinc-400">熟练使用 Codex、Claude Code、OpenCode 等 AI 编程工具，通过 VibeCoding 模式提升开发效率</p>
              </div>
            </div>
            <div class="flex items-start gap-3">
              <span class="text-xl">&#9889;</span>
              <div>
                <p class="text-white font-semibold">全栈工程</p>
                <p class="text-sm text-zinc-400">前端 Vue 3 + 后端 SpringBoot + 大数据 Hadoop，致力于成为 AI 时代的全栈工程师</p>
              </div>
            </div>
            <div class="flex items-start gap-3">
              <span class="text-xl">&#127919;</span>
              <div>
                <p class="text-white font-semibold">AI 实习生</p>
                <p class="text-sm text-zinc-400">积极寻找 AI 项目实习机会，将 AI 能力与工程实践相结合</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
