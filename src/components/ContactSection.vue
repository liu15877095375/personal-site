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

const contactItems = [
  {
    label: 'Email',
    value: 'liuzhenyuan2004@qq.com',
    href: 'mailto:liuzhenyuan2004@qq.com',
    icon: `<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>`,
  },
  {
    label: 'Phone',
    value: '15877095375',
    href: 'tel:15877095375',
    icon: `<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" /></svg>`,
  },
  {
    label: 'GitHub',
    value: 'github.com/liu15877095375',
    href: 'https://github.com/liu15877095375',
    icon: `<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" clip-rule="evenodd"/></svg>`,
  },
]
</script>

<template>
  <section id="contact" ref="section" class="py-24 md:py-32 px-6">
    <div class="max-w-4xl mx-auto text-center">
      <div :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <p class="text-sm font-medium text-violet-400 tracking-widest uppercase mb-4">Contact</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-4">
          联系我
        </h2>
        <p class="text-zinc-400 mb-12 max-w-lg mx-auto">
          如果你对我的项目感兴趣，或者有 AI 实习 / 项目合作机会，欢迎随时联系！
        </p>
      </div>

      <div class="flex flex-wrap justify-center gap-4 md:gap-6">
        <a
          v-for="(item, ii) in contactItems"
          :key="item.label"
          :href="item.href"
          target="_blank"
          :class="[
            'flex items-center gap-3 px-6 py-4 rounded-2xl glass card-hover transition-all duration-700 group',
            visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
          ]"
          :style="{ transitionDelay: `${200 + ii * 100}ms` }"
        >
          <span class="text-violet-400 group-hover:text-violet-300 transition-colors duration-300" v-html="item.icon"></span>
          <div class="text-left">
            <p class="text-xs text-zinc-500">{{ item.label }}</p>
            <p class="text-sm text-zinc-300 group-hover:text-white transition-colors duration-300">{{ item.value }}</p>
          </div>
          <svg class="w-4 h-4 text-zinc-600 group-hover:text-zinc-400 transition-colors duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
          </svg>
        </a>
      </div>
    </div>
  </section>
</template>
