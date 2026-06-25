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
    }, { threshold: 0.15 })
  }
})

const skillCategories = [
  {
    title: 'AI & 效率工具',
    icon: '&#129302;',
    skills: [
      { name: 'Claude Code', level: 90 },
      { name: 'Codex', level: 85 },
      { name: 'OpenCode', level: 80 },
      { name: 'OpenClaw', level: 78 },
    ],
  },
  {
    title: '编程语言',
    icon: '&#128187;',
    skills: [
      { name: 'Java', level: 80 },
      { name: 'C / C++', level: 75 },
      { name: 'SQL', level: 78 },
    ],
  },
  {
    title: '框架 & 基础设施',
    icon: '&#127959;',
    skills: [
      { name: 'Vue 3', level: 82 },
      { name: 'SpringBoot', level: 78 },
      { name: 'Hadoop', level: 70 },
      { name: 'MySQL', level: 76 },
      { name: 'Git', level: 80 },
    ],
  },
  {
    title: '通用能力',
    icon: '&#128161;',
    skills: [
      { name: 'Word / Excel / PPT', level: 85 },
      { name: '技术文档写作', level: 78 },
      { name: '团队协作', level: 82 },
      { name: '算法能力', level: 72 },
    ],
  },
]
</script>

<template>
  <section id="skills" ref="section" class="py-24 md:py-32 px-6 bg-zinc-900/30">
    <div class="max-w-4xl mx-auto">
      <div :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <p class="text-sm font-medium text-blue-400 tracking-widest uppercase mb-4">Skills</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-12">
          技能矩阵
        </h2>
      </div>

      <div class="grid md:grid-cols-2 gap-6">
        <div
          v-for="(category, ci) in skillCategories"
          :key="category.title"
          :class="[
            'glass rounded-2xl p-6 card-hover transition-all duration-700',
            visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
          ]"
          :style="{ transitionDelay: `${150 + ci * 100}ms` }"
        >
          <h3 class="text-sm font-semibold text-white mb-5 flex items-center gap-2">
            <span v-html="category.icon"></span>
            {{ category.title }}
          </h3>
          <div class="space-y-3.5">
            <div v-for="skill in category.skills" :key="skill.name">
              <div class="flex justify-between text-sm mb-1.5">
                <span class="text-zinc-300">{{ skill.name }}</span>
                <span class="text-zinc-500 text-xs">{{ skill.level }}%</span>
              </div>
              <div class="h-1.5 bg-zinc-800 rounded-full overflow-hidden">
                <div
                  class="h-full rounded-full bg-gradient-to-r from-violet-500 to-indigo-500 transition-all duration-1000 ease-out"
                  :style="{ width: visible ? `${skill.level}%` : '0%', transitionDelay: `${300 + ci * 100}ms` }"
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
