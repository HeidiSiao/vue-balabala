<template>
  <h3>
    Test.3- <code>v-if </code>靜態切換｜進階動態元件切換
    <code>&lt;component :is="currentView"&gt;&lt;/component&gt;</code>
  </h3>
  <button @click="viewToggle(1)">顯示單向綁定</button>
  <button @click="viewToggle(2)">顯示雙向綁定</button>
  <button @click="viewToggle(0)">清空畫面</button>

  <div class="containerA" v-if="view === 1">
    <p>資料綁定(單向)</p>
    {{ data }}
  </div>

  <div class="containerB" v-if="view === 2">
    <p>資料綁定(雙向)</p>
    <input type="text" v-model="text" />
    <p>{{ text }}</p>
  </div>

  <div v-else></div>
  <!-- 這樣才是完整的判斷式 -->
</template>

<script setup>
import { ref } from 'vue';
const data = ref('單向綁定');
const text = ref('');
const view = ref(1);
const viewToggle = (index) => {
  view.value = index;
};
</script>

<style scoped>
.containerA {
  border: 2px solid salmon;
  margin: 8px 0;
}

.containerB {
  border: 2px solid skyblue;
  margin: 8px 0;
}
</style>
