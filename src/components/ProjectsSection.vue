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

const certificates = [
  { src: import.meta.env.BASE_URL + '1.png' },
  { src: import.meta.env.BASE_URL + '2.jpg' },
  { src: import.meta.env.BASE_URL + '3.png' },
]

const selected = ref<number | null>(null)
</script>

<template>
  <section id="projects" ref="section" class="py-24 md:py-32 px-6 bg-zinc-900/30">
    <div class="max-w-4xl mx-auto">
      <div :class="['transition-all duration-700', visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8']">
        <p class="text-sm font-medium text-violet-400 tracking-widest uppercase mb-4">Certificates</p>
        <h2 class="text-3xl md:text-4xl font-bold text-white mb-12">
          证书展示
        </h2>
      </div>

      <div class="grid md:grid-cols-3 gap-6">
        <div
          v-for="(cert, ci) in certificates"
          :key="cert.src"
          :class="[
            'glass rounded-2xl overflow-hidden card-hover group cursor-pointer transition-all duration-700',
            visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'
          ]"
          :style="{ transitionDelay: `${150 + ci * 100}ms` }"
          @click="selected = ci"
        >
          <div class="aspect-[3/4] overflow-hidden">
            <img
              :src="cert.src"
              :alt="'证书 ' + (ci + 1)"
              class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
              loading="lazy"
            />
          </div>
        </div>
      </div>
    </div>

    <!-- Lightbox -->
    <Teleport to="body">
      <Transition
        enter-active-class="transition duration-300 ease-out"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
        leave-active-class="transition duration-200 ease-in"
        leave-from-class="opacity-100"
        leave-to-class="opacity-0"
      >
        <div
          v-if="selected !== null"
          class="fixed inset-0 z-50 bg-black/90 backdrop-blur-sm flex items-center justify-center p-4"
          @click="selected = null"
        >
          <button
            class="absolute top-6 right-6 text-white/60 hover:text-white transition-colors"
            @click="selected = null"
          >
            <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
          <img
            :src="certificates[selected].src"
            :alt="'证书 ' + (selected + 1)"
            class="max-w-full max-h-[90vh] object-contain rounded-lg"
            @click.stop
          />
        </div>
      </Transition>
    </Teleport>
  </section>
</template>
