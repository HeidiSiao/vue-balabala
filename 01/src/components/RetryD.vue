<script setup>
import { ref, computed } from 'vue';

// 原始資料
const msg = ref('Try again');
const addHandler = () => {
  msg.value += '!';
};

// const toggleHandler = () => {
//   msg.value = msg.value.split('').reverse().join('');
// };

// 畫面是否反轉的狀態標記
const isReverse = ref(false);
const toggleHandler = () => {
  isReverse.value = !isReverse.value;
};
// 根據原始資料與狀態切換而計算出的畫面內容
const displayMsg = computed(() => {
  return isReverse.value ? msg.value.split('').reverse().join('') : msg.value;
});
</script>

<template>
  <h2 class="test-word">{{ displayMsg }}</h2>
  <button class="try-btn" type="button" @click="addHandler">Append</button>
  <button class="try-btn" type="button" @click="toggleHandler">Reverse</button>
</template>

<style scoped>
.test-word {
  font-size: 32px;
  margin: 6px;
  color: pink;
}

.try-btn {
  margin-inline: 4px;
}
</style>
