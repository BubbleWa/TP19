<template>
  <div class="scambot-page">
    <!-- 标题 -->
    <div class="header-card">
      <h2>🤖 ScamDetector</h2>
      <p>
        Hi! I’m ScamMate, your scam-spotting buddy.<br>
        Paste a suspicious message or upload a screenshot—I’ll flag risks for you.
      </p>
    </div>

    <!-- 聊天框 -->
    <div class="chat-box">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        class="message-wrapper"
        :class="msg.type"
      >
        <!-- 机器人头像 -->
        <img
          v-if="msg.type === 'bot'"
          src="/bot.png"
          alt="Bot"
          class="avatar"
        />
        <!-- 用户头像 -->
        <div v-else class="avatar user-avatar">U</div>

        <!-- 消息气泡 -->
        <div class="message" :class="msg.type" v-html="msg.text"></div>
      </div>
    </div>

    <!-- 输入框 -->
    <div class="input-box">
      <input
        v-model="userInput"
        placeholder="Paste text or upload screenshot..."
        @keyup.enter="analyzeMessage"
      />
      <button @click="analyzeMessage">Detect</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"

const userInput = ref("")
const messages = ref([
  { type: "bot", text: "👋 Hi, paste a message and I'll check if it's a scam!" }
])

const scamKeywords = ["prize", "urgent", "click", "verify", "bank", "password", "link"]

const analyzeMessage = () => {
  if (!userInput.value.trim()) return

  messages.value.push({ type: "user", text: userInput.value })

  let lower = userInput.value.toLowerCase()
  let risk = scamKeywords.some(k => lower.includes(k))

  if (risk) {
    messages.value.push({
      type: "bot",
      text: `
        ⚠️ <strong>Detected: Likely Scam – High Risk</strong><br>
        <ul>
          <li>Suspicious keywords detected</li>
          <li>Sense of urgency or unusual link</li>
          <li>Possible phishing attempt</li>
        </ul>
        ✅ Recommended action: <strong>Do not click, block sender</strong>
      `
    })
  } else {
    messages.value.push({
      type: "bot",
      text: "✅ Looks safe! No scam keywords detected."
    })
  }

  userInput.value = ""
}
</script>

<style scoped>
.scambot-page {
  background: #f3e8ff;
  min-height: 100vh;
  padding: 20px;
  font-size: 1rem; /* 默认字体 */
}

/* ===== 标题 ===== */
.header-card {
  background: #7c3aed;
  color: white;
  text-align: center;
  padding: 24px 16px;
  border-radius: 12px;
  margin-bottom: 20px;
}
.header-card h2 {
  font-size: 1.8rem;
  margin-bottom: 10px;
}
.header-card p {
  font-size: 1rem;
  line-height: 1.6;
}
@media (min-width: 768px) {
  .header-card h2 { font-size: 2.4rem; }
  .header-card p { font-size: 1.3rem; }
}

/* ===== 聊天区域 ===== */
.chat-box {
  background: white;
  border-radius: 12px;
  padding: 16px;
  min-height: 300px;
  max-width: 900px;
  margin: 0 auto 20px auto;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  overflow-y: auto;
  font-size: 1rem;
}
@media (min-width: 768px) {
  .chat-box { font-size: 1.2rem; padding: 20px; }
}

/* 单条消息包装 */
.message-wrapper {
  display: flex;
  align-items: flex-start;
  margin: 12px 0;
  gap: 10px;
}
.message-wrapper.bot { flex-direction: row; }
.message-wrapper.user { flex-direction: row-reverse; }

/* 头像 */
.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}
.user-avatar {
  background: #6366f1;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1rem;
}
@media (min-width: 768px) {
  .avatar { width: 50px; height: 50px; }
  .user-avatar { font-size: 1.4rem; }
}

/* 消息气泡 */
.message {
  padding: 12px 16px;
  border-radius: 12px;
  max-width: 90%; /* 小屏更宽一点 */
  word-break: break-word;
  font-size: 1rem;
}
.message.bot {
  background: #f5f3ff;
  border-left: 5px solid #7c3aed;
}
.message.user {
  background: #e0e7ff;
  text-align: right;
}
@media (min-width: 768px) {
  .message { font-size: 1.2rem; max-width: 70%; }
}

/* ===== 输入框 ===== */
.input-box {
  display: flex;
  flex-wrap: wrap; /* 小屏时按钮换行 */
  gap: 10px;
  max-width: 900px;
  margin: 0 auto;
}
.input-box input {
  flex: 1;
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #ccc;
  font-size: 1rem;
}
.input-box button {
  background: #7c3aed;
  color: white;
  border: none;
  padding: 12px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  font-size: 1rem;
}
.input-box button:hover {
  background: #5b21b6;
}
@media (min-width: 768px) {
  .input-box input { font-size: 1.2rem; }
  .input-box button { font-size: 1.2rem; padding: 14px 20px; }
}
</style>
