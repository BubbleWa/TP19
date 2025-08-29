<template>
  <div class="dashboard-page">
    <!-- 紫色标题卡片 -->
    <section class="insights-card">
      <h2>Interactive Scam Insights</h2>
      <p>
        Filter by date, state, loss type, and age group to see what’s happening
        near you, track losses, and spot trending scams—so you can act
        before scammers do.
      </p>
    </section>

    <!-- 白色内容区 -->
    <section class="dashboard-content">
      <!-- 筛选器 -->
      <div class="filters">
        <select><option>Date Range</option></select>
        <select><option>State</option></select>
        <select><option>Loss Type</option></select>
        <select><option>Age Group</option></select>
      </div>

      <!-- 图表卡片布局 -->
      <div class="charts-grid">
        <div class="chart-card big">Reports & Losses</div>
        <div class="chart-card">States</div>
        <div class="chart-card">Total Reports</div>
        <div class="chart-card">Devices</div>
        <div class="chart-card">Age Groups</div>
        <div class="chart-card">Scams by Type</div>
      </div>
    </section>

    <!-- 底部场景模拟 + 报告 -->
    <section class="scenario-section">
      <div class="scenario-card">
        <h3>Scenario Check</h3>
        <p>
          You receive an SMS: Australia Post – Delivery Notice. Parcel on hold. 
          Update address: <a href="#">https://auspost.live/Parcel</a>  
          Reply “Y” within 24 hours.
        </p>
        <p><strong>What’s the safest next step?</strong></p>
        <ul>
          <li>A: Tap link & verify address</li>
          <li>B: Open official AusPost app / website and check tracking</li>
          <li>C: Reply “Y” to activate link</li>
        </ul>
        <button class="check-btn">Check Answer</button>
      </div>

      <div class="scenario-card">
        <h3>Open official AusPost app / website and check tracking</h3>
        <p><strong>What’s correct:</strong></p>
        <ul>
          <li>Look-alike link</li>
          <li>Sense of urgency</li>
          <li>Request to reply</li>
          <li>Unknown number</li>
        </ul>
        <button class="block-btn">Report & Block</button>
        <button class="alt-btn">Try another scenario</button>
      </div>
    </section>
  </div>
</template>

<script setup>
// 以后这里会接 API 替换内容
</script>

<style scoped>
.dashboard-page {
  background: #f3e8ff; /* 整个背景淡紫色 */
  min-height: 100vh;
  padding: 20px;
}

/* ===== 紫色标题卡片 ===== */
.insights-card {
  background: linear-gradient(to right, #5b21b6, #7c3aed);
  color: white;
  text-align: center;
  padding: 40px 20px;
  border-radius: 12px;
  max-width: 1200px;
  margin: 0 auto 20px auto;
  box-shadow: 0 4px 10px rgba(0,0,0,0.15);
}
.insights-card h2 {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 12px;
}
.insights-card p {
  font-size: 1rem;
  line-height: 1.6;
  max-width: 900px;
  margin: 0 auto;
}
@media (min-width: 768px) {
  .insights-card h2 { font-size: 2.8rem; }
  .insights-card p { font-size: 1.6rem; }
}

/* ===== 白色内容区 ===== */
.dashboard-content {
  background: white;
  padding: 20px;
  border-radius: 12px;
  max-width: 1200px;
  margin: 0 auto 20px auto;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

/* 筛选器 */
.filters {
  display: flex;
  flex-wrap: wrap; /* 小屏幕自动换行 */
  gap: 12px;
  margin-bottom: 20px;
}
.filters select {
  flex: 1;
  min-width: 140px;
  padding: 10px 14px;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 1rem;
}
@media (min-width: 768px) {
  .filters select { font-size: 1.2rem; }
}

/* 图表卡片布局 */
.charts-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}
.chart-card {
  background: #fff;
  border-radius: 10px;
  padding: 20px;
  min-height: 140px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.08);
  font-size: 1.2rem;
  font-weight: bold;
  display: flex;
  align-items: center;
  justify-content: center;
}
.chart-card.big {
  min-height: 220px;
}
@media (min-width: 900px) {
  .charts-grid {
    grid-template-columns: 2fr 1fr 1fr;
    grid-template-rows: auto auto;
  }
  .chart-card.big {
    grid-row: span 2;
    min-height: 280px;
  }
  .chart-card { font-size: 1.4rem; }
}

/* ===== 场景模拟部分 ===== */
.scenario-section {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
}
@media (min-width: 900px) {
  .scenario-section {
    grid-template-columns: 1fr 1fr;
  }
}
.scenario-card {
  background: #ede9fe; /* 淡紫色卡片 */
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 3px 8px rgba(0,0,0,0.1);
}
.scenario-card h3 {
  font-size: 1.4rem;
  margin-bottom: 10px;
  color: #4c1d95;
}
.scenario-card p, .scenario-card li {
  font-size: 1rem;
  margin-bottom: 6px;
}
@media (min-width: 768px) {
  .scenario-card h3 { font-size: 1.8rem; }
  .scenario-card p, .scenario-card li { font-size: 1.2rem; }
}
.scenario-card ul {
  padding-left: 18px;
  margin-bottom: 12px;
}
.check-btn,
.block-btn,
.alt-btn {
  padding: 10px 18px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 600;
  border: none;
}
.check-btn {
  background: #6366f1;
  color: white;
}
.check-btn:hover { background: #4338ca; }
.block-btn {
  background: #22c55e;
  color: white;
  margin-right: 10px;
}
.block-btn:hover { background: #16a34a; }
.alt-btn {
  background: #f3f4f6;
  color: #333;
}
.alt-btn:hover { background: #e5e7eb; }
</style>
