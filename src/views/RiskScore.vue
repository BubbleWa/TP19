<template>
  <div class="risk-page">
    <!-- 页面标题 -->
    <section class="risk-header">
      <h2>Risk Score Measure</h2>
      <p>
        CyberMate’s Risk Score helps you understand your personal exposure.  
        Based on your online activity and scam history, get a score that shows your digital risk level.
      </p>
    </section>

    <!-- 风险仪表盘卡片 -->
    <section class="risk-card">
      <img src="/risk-meter.png" alt="Risk Meter" class="risk-image" />
      <div class="risk-info">
        <h3>Your Risk Score</h3>
        <p>This is a placeholder — will be powered by API later.</p>
        <button class="risk-btn">Measure Now</button>
      </div>
    </section>
  </div>
</template>

<script setup>
// 未来可以在这里加 API 逻辑
</script>

<style scoped>
/* 页面背景 */
.risk-page {
  background: #f3e8ff;   /* 淡紫色背景 */
  min-height: 100vh;
  padding: 100px 20px 20px; /* 上面留 100px 避免挡住导航栏 */
}

/* 标题部分 */
.risk-header {
  text-align: center;
  margin-bottom: 30px;
}
.risk-header h2 {
  font-size: 2.5rem;
  font-weight: bold;
  color: #4c1d95;
  margin-bottom: 10px;
}
.risk-header p {
  font-size: 1.2rem;
  max-width: 700px;
  margin: 0 auto;
  color: #333;
}

/* 风险卡片 */
.risk-card {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 40px;
  background: white;
  padding: 40px;
  border-radius: 16px;
  max-width: 900px;
  margin: 0 auto;
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
}

.risk-image {
  width: 200px;
  height: auto;
}

.risk-info h3 {
  font-size: 1.8rem;
  font-weight: bold;
  margin-bottom: 12px;
}
.risk-info p {
  font-size: 1.1rem;
  margin-bottom: 20px;
  color: #555;
}

.risk-btn {
  background: #facc15;
  padding: 12px 24px;
  border-radius: 10px;
  font-size: 1.2rem;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}
.risk-btn:hover {
  background: #eab308;
  transform: translateY(-2px);
}
</style>
