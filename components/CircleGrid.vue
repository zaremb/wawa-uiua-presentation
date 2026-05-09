<template>
  <div class="absolute inset-0 overflow-hidden pointer-events-none select-none flex items-center justify-center" style="z-index: -1" aria-hidden="true">
    <div
      class="grid"
      :style="{
        gridTemplateColumns: `repeat(${cols}, 1fr)`,
        gridTemplateRows: `repeat(${rows}, 1fr)`,
        width: '80%',
        height: '70%',
        gap: gap + 'px',
      }"
    >
      <div
        v-for="i in rows * cols"
        :key="i"
        class="circle-dot"
        :style="{
          width: size + 'px',
          height: size + 'px',
          opacity: opacity,
          animationDelay: (i * 0.03) + 's',
        }"
      />
    </div>
  </div>
</template>

<script setup>
defineProps({
  rows: { type: Number, default: 7 },
  cols: { type: Number, default: 9 },
  size: { type: Number, default: 18 },
  gap: { type: Number, default: 0 },
  opacity: { type: Number, default: 0.85 },
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
