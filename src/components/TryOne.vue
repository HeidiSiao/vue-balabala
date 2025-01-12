<template>
  <h3>Test.1- <code>setInterval</code> 5秒 要把答案藏起來</h3>
  <div>
    <!-- 使用計算屬性來處理顯示的文本 -->
    <button @click="toggleAnswer">{{ buttonText }}答案 ＆ 計時器：{{ timer }} 秒</button>
    <p v-if="showAnswer && timer > 0">我放一個倒數計時器：{{ timer }}秒</p>
    <p v-if="showAnswer && timer > 0">答案答案答案在這裡</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const showAnswer = ref(false); // 初始值設為 false
const timer = ref(5); //設定初始倒數秒數為 5
let timerId = null;

// 計算屬性來動態返回按鈕文本
//將 buttonText 的值 同時依賴於 showAnswer 和timer的狀態
const buttonText = computed(() => {
  if (showAnswer.value) {
    return timer.value > 0 ? '隱藏' : '顯示';
  } else {
    return '顯示';
  }
});

// 切換 showAnswer 的值
// const toggleAnswer = () => {
//   showAnswer.value = !showAnswer.value

//   if (showAnswer.value) {
//     countDown() //開始倒數
//   }
// }
const toggleAnswer = () => {
  if (showAnswer.value) {
    showAnswer.value = false;
    clearInterval(timerId); // 停止倒數計時
    timer.value = 5;
  } else {
    showAnswer.value = true;
    countDown(); // 開始倒數
  }
};

const countDown = () => {
  timer.value = 5;
  timerId = setInterval(() => {
    if (timer.value > 0) {
      timer.value -= 1;
    } else {
      clearInterval(timerId); //停止計時
      showAnswer.value = false; //停止顯示答案
    }
  }, 1000);
};
</script>
