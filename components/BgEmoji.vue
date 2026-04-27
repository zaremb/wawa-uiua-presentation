<template>
  <div class="absolute inset-0 overflow-hidden pointer-events-none select-none" style="z-index: 0" aria-hidden="true">
    <span
      v-for="item in items"
      :key="item.id"
      class="absolute"
      :style="{
        fontSize: item.size + 'px',
        left: item.x + '%',
        top: item.y + '%',
        opacity: item.opacity,
        animation: item.animation,
        animationDelay: item.delay + 's',
        animationDuration: item.duration + 's',
        animationFillMode: item.fillMode,
        animationIterationCount: item.iterationCount,
      }"
    >{{ emoji }}</span>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  emoji: { type: String, required: true },
  count: { type: Number, default: 5 },
  animate: { type: String, default: 'float' }, // float | fly | grow | drift
  opacity: { type: Number, default: 0.06 },
  seed: { type: Number, default: 42 },
})

// Simple seeded pseudo-random for deterministic layouts
function seededRandom(s) {
  let state = s
  return () => {
    state = (state * 1664525 + 1013904223) & 0xffffffff
    return (state >>> 0) / 0xffffffff
  }
}

const flyDirections = ['emoji-fly-0', 'emoji-fly-1', 'emoji-fly-2', 'emoji-fly-3']

const baseAnimations = {
  float: 'emoji-float',
  grow: 'emoji-grow',
  drift: 'emoji-drift',
}

const items = computed(() => {
  const rand = seededRandom(props.seed)
  const isGrow = props.animate === 'grow'
  const isFly = props.animate === 'fly'

  return Array.from({ length: props.count }, (_, i) => {
    const animName = isFly
      ? flyDirections[Math.floor(rand() * flyDirections.length)]
      : baseAnimations[props.animate] || baseAnimations.float

    return {
      id: i,
      // fly: left=0 so animation translate controls full horizontal travel; top=random height
      x: isFly ? 0 : rand() * 90 + 5,
      y: isFly ? rand() * 70 + 10 : rand() * 80 + 10,
      size: 30 + rand() * 30,
      opacity: props.opacity * (0.6 + rand() * 0.4),
      delay: isGrow ? rand() * 5 : -(rand() * (12 + rand() * 20)),
      duration: isGrow ? 3 + rand() * 3 : isFly ? 25 + rand() * 20 : 12 + rand() * 20,
      animation: `${animName} ${isFly ? 'linear' : 'ease-in-out'}`,
      fillMode: 'both',
      iterationCount: isGrow ? '1' : 'infinite',
    }
  })
})
</script>

<style>
@keyframes emoji-float {
  0% { transform: translateY(0) rotate(-3deg); }
  50% { transform: translateY(-20px) rotate(5deg); }
  100% { transform: translateY(0) rotate(-3deg); }
}

/* Fly in 4 directions — no opacity animation (inline opacity controls transparency) */
/* 🚀 default points NE (~45°). Rotations orient nose in direction of flight. */
@keyframes emoji-fly-0 {
  /* Left → Right (east): rotate 45° so nose points right */
  0% { transform: translateX(-80px) rotate(45deg); }
  100% { transform: translateX(105vw) rotate(45deg); }
}
@keyframes emoji-fly-1 {
  /* Right → Left (west): rotate 225° so nose points left */
  0% { transform: translateX(105vw) rotate(225deg); }
  100% { transform: translateX(-80px) rotate(225deg); }
}
@keyframes emoji-fly-2 {
  /* Bottom-left → Top-right (NE): 0° — default orientation */
  0% { transform: translate(-80px, 40vh) rotate(0deg); }
  100% { transform: translate(105vw, -40vh) rotate(0deg); }
}
@keyframes emoji-fly-3 {
  /* Top-right → Bottom-left (SW): rotate 180° */
  0% { transform: translate(105vw, -40vh) rotate(180deg); }
  100% { transform: translate(-80px, 40vh) rotate(180deg); }
}

@keyframes emoji-grow {
  0% { transform: scale(0); }
  50% { transform: scale(1.1); }
  80% { transform: scale(0.95); }
  100% { transform: scale(1); }
}

@keyframes emoji-drift {
  0% { transform: translateX(0) translateY(0) rotate(0deg); }
  25% { transform: translateX(15px) translateY(-10px) rotate(3deg); }
  50% { transform: translateX(-10px) translateY(-20px) rotate(-2deg); }
  75% { transform: translateX(20px) translateY(-5px) rotate(4deg); }
  100% { transform: translateX(0) translateY(0) rotate(0deg); }
}
</style>
