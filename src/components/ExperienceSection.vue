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

const experiences = [
  {
    role: 'HDFS 分布式⽹盘系统',
    company: '团队负责⼈',
    period: '2026-03 〜 2026-06',
    description: '带队落地 Vibe Coding 开发模式，通过CC Switch接⼊DeepSeek API，以 Codex 为主要 AI⼯具，搭建分布式存储架构。',
    highlights: [
      '制定Prompt编写规范；借助 Codex 进⾏代码⽣成、HDFS 排错、IO 性能优化，建⽴ AI 代码⼈⼯审核机制',
      'Vue3+SpringBoot+MySQL 开发⽹盘全栈功能，制定团队 AI 编码 + Git 协作流程',
      '借助 AI ⽣成单元测试、部署脚本，完成多节点 HDFS 集群部署',
    ],
    tags: ['Vue3', 'SpringBoot', 'HDFS', 'Codex', 'DeepSeek API'],
  },
  {
    role: '个⼈⽹站',
    company: '独⽴开发',
    period: '2026-06 〜 至今',
    description: '通过CC Switch接⼊DeepSeek API，以Claude Code为主要AI⼯具，开发了个⼈介绍⽹站并部署到GitHub Pages。',
    highlights: [
      '⽹站地址：https://liu15877095375.github.io/personal-site/',
    ],
    tags: ['Claude Code', 'DeepSeek API', 'Vue3', 'GitHub Pages'],
  },
]
</script>

<template>
  <section id="experience" ref="section" class="py-24 md:py-32 px-6">
    <div class="max-w-4xl mx-auto">
      <div :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <p class="text-sm font-medium text-green-400 tracking-widest uppercase mb-4">Experience</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-12">
          项目经历
        </h2>
      </div>

      <div class="relative">
        <!-- Timeline line -->
        <div class="absolute left-5 md:left-6 top-2 bottom-2 w-px bg-gradient-to-b from-violet-500/50 via-indigo-500/50 to-transparent" />

        <div class="space-y-12">
          <div
            v-for="(exp, ei) in experiences"
            :key="exp.company"
            :class="['relative pl-14 md:pl-16 transition-all duration-700', visible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-8']"
            :style="{ transitionDelay: `${200 + ei * 200}ms` }"
          >
            <!-- Timeline dot -->
            <div class="absolute left-3 md:left-4 top-1 w-4 h-4 rounded-full bg-gradient-to-br from-violet-500 to-indigo-500 shadow-lg shadow-violet-500/30 flex items-center justify-center">
              <div class="w-2 h-2 rounded-full bg-white" />
            </div>

            <div class="glass rounded-2xl p-6 md:p-8 card-hover">
              <div class="flex flex-wrap items-start justify-between gap-2 mb-3">
                <h3 class="text-lg font-bold text-white">{{ exp.role }}</h3>
                <span class="text-xs text-zinc-500 px-3 py-1 rounded-full bg-zinc-800/50">{{ exp.period }}</span>
              </div>
              <p class="text-sm text-violet-400 font-medium mb-2">{{ exp.company }}</p>
              <p class="text-sm text-zinc-400 leading-relaxed mb-4">{{ exp.description }}</p>
              <ul class="space-y-2 mb-4">
                <li v-for="h in exp.highlights" :key="h" class="text-sm text-zinc-300 flex items-start gap-2">
                  <span class="text-green-400 mt-1.5 w-1.5 h-1.5 rounded-full bg-green-400 flex-shrink-0" />
                  {{ h }}
                </li>
              </ul>
              <div class="flex flex-wrap gap-2">
                <span
                  v-for="tag in exp.tags" :key="tag"
                  class="text-xs px-3 py-1 rounded-full bg-zinc-800 text-zinc-400 border border-zinc-700/50"
                >{{ tag }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
