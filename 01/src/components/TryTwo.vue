<template>
  <h3>Test.2- <code>input</code> 動起來的搜尋框框 + nextTick()</h3>
  <div class="form-wrap">
    <div class="form-field">
      <input type="text" id="name" autocomplete="off" class="form-control" placeholder=" " />
      <label for="name">Enter your name</label>
    </div>
    <div class="form-field">
      <input type="text" id="password" autocomplete="off" class="form-control" placeholder=" " />
      <label for="password">Enter your password | 密碼功能GG</label>
    </div>

    <div class="form-field">
      <input
        @keydown.enter="putMessage"
        type="text"
        id="message"
        autocomplete="off"
        class="form-control"
        placeholder=" "
      />
      <label for="message">Message List</label>
    </div>
    <div class="messages">
      <div v-for="(message, index) in messages" :key="index">{{ message }}</div>
    </div>
  </div>
</template>

<script setup>
import { nextTick, ref } from 'vue';
const messages = ref([]);
const putMessage = async (event) => {
  // 把觸發事件的input元素的輸入值放進陣列
  messages.value.push(event.target.value);
  event.target.value = '';
  // 開 DOM
  await nextTick(() => {
    const showMessage = document.querySelector('.messages');
    showMessage.scrollTop = showMessage.scrollHeight;
  });
  // scrollTop 控制內容距離容器頂部的工具（初始0，也就是可視範圍的起點）
  // 可視範圍：能看到的內容高度，也就是我設定的容器height
  // scrollHeight 是容器內「內容的整個高度」包括「可視範圍之外」
  // scrollTop(捲軸距離容器上方的距離) 調整成 內容的整個高度，就可以顯示最底部的最新輸入值！
  // push後馬上DOM，scrollTop新值反應不過來，DOM更新的內容還在排隊
};
</script>

<style scoped>
.form-wrap {
  width: 100%;
}
/* 欄位容器＝我的定位基準 */
.form-field {
  position: relative;
  margin-bottom: 8px;
}
/* 欄位樣式 */
.form-control {
  width: 100%;
  padding: 20px 15px 10px;

  font-size: 20px;
  border: 2px solid #ccc;
  border-radius: 4px;
  outline: none;
  background-color: #69b0ac;
  /* 標籤（label）依據此定位 */
  position: relative;
}
/* 初始標籤位置 */
label {
  position: absolute;
  top: 50%;
  left: 10px;
  font-size: 16px;
  color: lemonchiffon;
  transform: translateY(-50%);
  transition: all 0.2s ease;
  /* 防止點擊標籤 */
  pointer-events: none;
}

/* 當輸入框聚焦 或 使用者有輸入內容時 樣式狀態 */
.form-control:focus + label,
.form-control:not(:placeholder-shown) + label {
  top: calc(50% - 18px);
  font-size: 12px;
  font-weight: bold;
}

/* 輸入框聚焦時的樣式 */
.form-control:focus {
  border-color: #066e3e;
  box-shadow: 0 0 3px rgba(0, 0, 0, 0.5);
}

.form-control:not(:placeholder-shown) {
  color: #434343;
  font-weight: bold;
}
</style>

<style scoped>
.messages {
  height: 70px;
  padding-inline: 4px;
  overflow-y: scroll; /* 該區顯示垂直滾動條（即使沒有內容） */
  color: #066e3e;
  background-color: lemonchiffon;
}
</style>
