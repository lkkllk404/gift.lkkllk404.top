<template>
  <div class="background-animation">
    <div class="gradient-bg"></div>

    <div
      v-for="bubble in bubbles"
      :key="bubble.id"
      class="bubble"
      :style="{
        left: bubble.x + 'px',
        top: bubble.y + 'px',
        width: bubble.size + 'px',
        height: bubble.size + 'px',
        animationDelay: bubble.delay + 's',
        animationDuration: bubble.duration + 's'
      }"
    ></div>

    <Teleport to="body">
      <mainContent />
    </Teleport>
  </div>
</template>

<script setup>
import { ref, onMounted, Teleport } from 'vue'
import mainContent from './mainContent.vue';

const bubbles = ref([])
const random = (min, max) => Math.random() * (max - min) + min

const initBubbles = () => {
  for (let i = 0; i < 12; i++) {
    bubbles.value.push({
      id: i,
      x: random(0, window.innerWidth),
      y: random(window.innerHeight, window.innerHeight + 100),
      size: random(20, 60),
      delay: random(0, 8),
      duration: random(10, 20)
    })
  }
}

onMounted(() => {
  initBubbles()
})
</script>

<style scoped>
.background-animation {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  z-index: -1;
  pointer-events: none;
}

.gradient-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    45deg,
    #ff9a9e,
    #fecfef,
    #a8edea,
    #fed6e3
  );
  background-size: 400% 400%;
  animation: gradientShift 20s ease-in-out infinite;
}

@keyframes gradientShift {
  0% {
    background-position: 0% 50%;
  }
  25% {
    background-position: 100% 50%;
  }
  50% {
    background-position: 100% 100%;
  }
  75% {
    background-position: 50% 100%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.bubble {
  position: absolute;
  background: rgba(255, 255, 255, 0.4);
  border: 2px solid rgba(255, 255, 255, 0.6);
  border-radius: 50%;
  animation: floatBubble infinite linear;
  backdrop-filter: blur(1px);
  box-shadow: 
    inset 0 0 20px rgba(255, 255, 255, 0.3),
    0 0 20px rgba(255, 255, 255, 0.2);
}

@keyframes floatBubble {
  0% {
    transform: translateY(0) scale(1);
    opacity: 0.9;
  }
  50% {
    transform: translateY(-50vh) scale(1.1);
    opacity: 0.7;
  }
  100% {
    transform: translateY(-100vh) scale(0.8);
    opacity: 0;
  }
}

/* 一些额外的视觉效果 */
.background-animation::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle at 20% 80%,
    rgba(255, 182, 193, 0.3) 0%,
    transparent 50%
  ),
  radial-gradient(
    circle at 80% 20%,
    rgba(173, 216, 230, 0.3) 0%,
    transparent 50%
  );
  animation: pulseGlow 8s ease-in-out infinite;
}

@keyframes pulseGlow {
  0%, 100% {
    opacity: 0.5;
  }
  50% {
    opacity: 0.8;
  }
}
</style>