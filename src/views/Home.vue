<template>
  <!-- 最外层容器：整页背景 -->
  <div class="page-wrapper">
    <!-- Hero Section -->
    <section class="hero-banner">
      <div class="hero-overlay">
        <div class="hero-content">
          <h2 class="hero-title">
            Stay Safe Online with <span class="highlight">CyberMate</span>
          </h2>
          <p class="hero-subtitle">
            Your trusted mate for spotting scams, boosting digital skills, and staying secure.
          </p>
          <!-- 预留跳转，你说第一个还没决定，所以我留空 -->
          <button class="hero-button">Get Started</button>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section class="about-section">
      <div class="about-container">
        <div class="about-text">
          <h3>About CyberMate</h3>
          <p>
            CyberMate empowers young Australians to recognise, avoid, and report scams.
            Through interactive dashboards, a scam detector bot, and a risk score tracker,
            we make online safety engaging and easy.
          </p>
        </div>

        <div class="about-stats">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="stat-card"
            :style="{ backgroundColor: stat.color }"
          >
            <h4>{{ stat.value }}</h4>
            <p>{{ stat.label }}</p>
          </div>
        </div>
      </div>

      <div class="explore-container">
        <button class="explore-btn" @click="goToDashboard">Explore Dashboard</button>
      </div>
    </section>

    <!-- ScamBot Section -->
    <section class="bot-section">
      <div class="bot-container">
        <div class="bot-image">
          <img src="/bot.png" alt="Scam Detector Bot" />
        </div>
        <div class="bot-text">
          <h3>
            Meet our <span class="highlight">Scam Detector Bot</span>
          </h3>
          <p>
            Just paste a suspicious message,<br />
            and our AI will instantly tell you if it looks like a scam.
          </p>
          <button class="bot-button" @click="goToScamBot">Explore ScamBot</button>
        </div>
      </div>
    </section>

    <!-- Risk Score Section -->
    <section class="risk-section">
      <div class="risk-container">
        <div class="risk-image">
          <img src="/risk-meter.png" alt="Risk Score Meter" />
        </div>
        <div class="risk-text">
          <h3>Risk Score Measure</h3>
          <p>
            CyberMate’s Risk Score helps you understand your personal exposure.
            Based on your online activity and scam history, get a score that
            shows your digital risk level.
          </p>
          <button class="risk-button" @click="goToRiskScore">Measure your Risk Score</button>
        </div>
      </div>
    </section>

    <!-- 右下角 ScamBot 浮窗 -->
    <div class="scambot-floating" @click="goToScamBot">
      <img src="/bot.png" alt="ScamBot" />
      <span>ScamBot</span>
    </div>

    <!-- 左下角语言切换器浮窗 -->
    <div class="language-switcher">
      <select v-model="selectedLang">
        <option value="en">English</option>
        <option value="jp">日本語</option>
        <option value="ar">العربية</option>
        <option value="zh">中文</option>
        <option value="es">Español</option>
        <option value="fr">Français</option>
      </select>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
import { useRouter } from "vue-router"

const stats = ref([
  { value: "$3.1B", label: "lost to scams in 2022", color: "#bae6fd" },
  { value: "47%", label: "victims aged 18–35", color: "#fecdd3" },
  { value: "47%", label: "aged 15–38", color: "#fecaca" },
  { value: "Top scams", label: "Phishing · Fake Jobs · Shopping", color: "#fde68a" }
])

// 语言选择
const selectedLang = ref("en")

// 路由跳转
const router = useRouter()
const goToDashboard = () => router.push("/dashboard")
const goToScamBot = () => router.push("/scambot")
const goToRiskScore = () => router.push("/riskscore")
</script>

<style scoped>
.page-wrapper {
  background-color: #f3e8ff;
  min-height: 100vh;
  padding: 20px 0;
}

/* ===== HERO ===== */
.hero-banner {
  background-image: url("/cyber-bg.png");
  background-size: cover;
  background-position: center;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}
.hero-overlay {
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.hero-content {
  text-align: center;
  max-width: 900px;
}
.hero-title {
  font-size: 4rem;
  font-weight: 800;
  color: white;
  margin-bottom: 20px;
  line-height: 1.3;
}
.highlight {
  color: #60a5fa;
}
.hero-subtitle {
  color: #e5e7eb;
  font-size: 1.8rem;
  margin-bottom: 28px;
}
.hero-button {
  background: #6366f1;
  color: white;
  padding: 14px 36px;
  font-size: 1.4rem;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}
.hero-button:hover {
  background: #4f46e5;
  transform: translateY(-3px);
}

/* ===== ABOUT ===== */
.about-section {
  background: white;
  padding: 50px 30px;
  border-radius: 16px;
  max-width: 1200px;
  margin: 40px auto;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
}
.about-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: center;
}
.about-text h3 {
  font-size: 2.8rem;
  font-weight: bold;
  margin-bottom: 16px;
}
.about-text p {
  font-size: 1.5rem;
  color: #444;
  line-height: 1.8;
}
.about-stats {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}
.stat-card {
  padding: 28px;
  border-radius: 14px;
  text-align: center;
  font-weight: bold;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.08);
}
.stat-card h4 {
  font-size: 2.6rem;
  margin-bottom: 10px;
}
.stat-card p {
  font-size: 1.4rem;
}
.explore-container {
  text-align: center;
  margin-top: 32px;
}
.explore-btn {
  background: #facc15;
  padding: 14px 34px;
  border-radius: 10px;
  font-size: 1.4rem;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}
.explore-btn:hover {
  background: #eab308;
  transform: translateY(-2px);
}

/* ===== BOT ===== */
.bot-section {
  background: linear-gradient(to right, #6366f1, #3b82f6, #06b6d4);
  padding: 60px 20px;
  border-radius: 16px;
  max-width: 1200px;
  margin: 40px auto;
  color: white;
}
.bot-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: center;
}
.bot-image img {
  width: 180px;
  height: auto;
  margin: 0 auto;
  display: block;
}
.bot-text h3 {
  font-size: 2.8rem;
  font-weight: bold;
  margin-bottom: 16px;
}
.bot-text .highlight {
  color: #facc15;
}
.bot-text p {
  font-size: 1.5rem;
  margin-bottom: 24px;
  line-height: 1.6;
}
.bot-button {
  background: #4f46e5;
  color: white;
  padding: 14px 32px;
  font-size: 1.4rem;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}
.bot-button:hover {
  background: #4338ca;
  transform: translateY(-3px);
}

/* ===== RISK SCORE ===== */
.risk-section {
  background: #f3f4f6;
  padding: 60px 20px;
  border-radius: 16px;
  max-width: 1200px;
  margin: 40px auto;
}
.risk-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: center;
}
.risk-image img {
  width: 200px;
  height: auto;
  margin: 0 auto;
  display: block;
}
.risk-text h3 {
  font-size: 2.4rem;
  font-weight: bold;
  margin-bottom: 16px;
}
.risk-text p {
  font-size: 1.3rem;
  line-height: 1.6;
  margin-bottom: 24px;
  color: #333;
}
.risk-button {
  background: #facc15;
  padding: 14px 34px;
  border-radius: 10px;
  font-size: 1.4rem;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}
.risk-button:hover {
  background: #eab308;
  transform: translateY(-2px);
}

/* ===== SCAMBOT FLOATING ===== */
.scambot-floating {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: #6d28d9;
  color: white;
  padding: 10px 14px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
  transition: all 0.3s ease;
}
.scambot-floating img {
  width: 30px;
  height: 30px;
}
.scambot-floating:hover {
  background: #4c1d95;
  transform: translateY(-3px);
}

/* ===== LANGUAGE SWITCHER ===== */
.language-switcher {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background: #6d28d9;
  padding: 8px 12px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
}
.language-switcher select {
  border: none;
  background: transparent;
  color: white;
  font-size: 1rem;
  font-weight: 500;
  outline: none;
  cursor: pointer;
}
.language-switcher select option {
  color: black;
}
</style>
