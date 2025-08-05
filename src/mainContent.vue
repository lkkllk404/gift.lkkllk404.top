<template>
  <div class="mainOverlay">
    <div class="mainContent" @click.stop>
      <h1 class="title">生日快乐喵喵喵！</h1>
      <h4 class="subtitle">——超喜欢猫猫的</h4>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['close']);
</script>

<style scoped>
.mainOverlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.mainContent {
  padding: 20px;
  border-radius: 5px;
  /*box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);*/
  max-width: 700px;
  width: 100%;
}

.title {
  text-align: center;
  font-size: 64px;
  color: #333;
}
.subtitle {
  text-align: right;
  font-size: 18px;
  color: #666;
}
</style>