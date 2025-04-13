<template>
  <h3>Test.4- <code>ref,computed</code> 原始資料|狀態標記|計算值</h3>
  <a target="_blank" class="a-link" href="#" @click.prevent="clickHandler">不能產生連結</a>
  <p class="target-msg">{{ displayMsg }}</p>
  <button class="btn-msg" type="button" @click="reverseHandler">Reverse</button>
  <button class="btn-msg" type="button" @click="appendHandler">Append</button>
</template>

<script setup>
import { ref, computed } from 'vue';

// 原始資料寫入時調整
const msg = ref('Have Fun');

// 讓 append 永遠是加在末尾
const isReverse = ref(false);

// 顯示資料 computed 可寫成三元
const displayMsg = computed(() => {
  if (isReverse.value) {
    return msg.value.split('').reverse().join('');
  } else {
    return msg.value;
  }
});

const clickHandler = () => {
  alert('嗨嗨被點擊了');
};
const appendHandler = () => {
  msg.value += '☺️';
};

// 點擊reverse 按鈕時
const reverseHandler = () => {
  isReverse.value = !isReverse.value;
};

// 改變東西的初始值 computed
// 笑臉的動作需要一起被翻轉
</script>

<style scoped>
.btn-msg {
  margin: 5px;
  display: block;
}

.a-link {
  display: inline-block;
  color: goldenrod;
  text-decoration: none;
  margin-inline: 6px;
}

.a-link:hover {
  color: lightcoral;
  text-decoration: dotted crimson underline;
}

.target-msg {
  color: silver;
  font-size: 32px;
  font-weight: bold;
  margin: 6px;
}
</style>
