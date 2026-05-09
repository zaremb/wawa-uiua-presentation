<template>
  <div v-if="visible" class="fixed inset-0 overflow-hidden pointer-events-none select-none flex items-center justify-center" style="z-index: 1" aria-hidden="true">
    <div class="relative" :style="{ width: '80%', height: '70%' }">
      <div
        v-for="(dot, i) in dots"
        :key="i"
        class="circle-dot absolute"
        :style="{
          width: size + 'px',
          height: size + 'px',
          opacity: opacity,
          left: dot.x + '%',
          top: dot.y + '%',
          animationDelay: (i * 0.03) + 's',
        }"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  rows: { type: Number, default: 7 },
  cols: { type: Number, default: 9 },
  size: { type: Number, default: 18 },
  opacity: { type: Number, default: 0.85 },
  delay: { type: Number, default: 0 },
})

const dots = computed(() => {
  const result = []
  const xStep = 100 / props.cols
  const yStep = 100 / props.rows
  for (let r = 0; r < props.rows; r++) {
    const offset = r % 2 === 1 ? xStep / 2 : 0
    for (let c = 0; c < props.cols; c++) {
      result.push({
        x: c * xStep + offset + xStep / 2 - (props.size / 20),
        y: r * yStep + yStep / 2 - (props.size / 20),
      })
    }
  }
  return result
})

const visible = ref(props.delay <= 0)
let timer = null

onMounted(() => {
  if (props.delay > 0) {
    timer = setTimeout(() => { visible.value = true }, props.delay * 1000)
  }
})

onUnmounted(() => {
  if (timer) clearTimeout(timer)
})
</script>

<style>
.circle-dot {
  border-radius: 50%;
  background: white;
  justify-self: center;
  align-self: center;
  transform: scale(0);
  animation: circle-pop 0.4s ease-out forwards;
}

@keyframes circle-pop {
  0% { transform: scale(0); }
  70% { transform: scale(1.1); }
  100% { transform: scale(1); }
}
</style>
