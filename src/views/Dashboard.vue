<template>
  <div class="dashboard-page">
    <div class="wrap">
      <!-- State selector row -->
      <section class="state-selector">
        <button class="state-btn act">ACT</button>
        <button class="state-btn nsw">NSW</button>
        <button class="state-btn nt">NT</button>
        <button class="state-btn qld">QLD</button>
        <button class="state-btn sa">SA</button>
        <button class="state-btn vic">VIC</button>
        <button class="state-btn wa">WA</button>
        <button class="state-btn tas">TAS</button>
      </section>

      <!-- Breaking news -->
      <section class="breaking-row">
        <span>BREAKING NEWS</span>
        <span>BREAKING NEWS</span>
        <span>BREAKING NEWS</span>
      </section>

      <!-- Top row: left / middle / right -->
      <section class="top-row-grid">
        <div class="card">
          <div class="card-head">
            <select class="scam-select"><option>Scam type</option></select>
          </div>
          <h3>Total Losses</h3>
          <p class="number">167B</p>
        </div>

        <div class="card big">
          <h3 class="center">20% Likely to Get Scam</h3>
          <p class="center subt">2 out of 10 faced financial loss through scam</p>
          <div class="chart-placeholder">[ Chart Placeholder ]</div>
        </div>

        <div class="card">
          <h3>Top Scams by Loss</h3>
          <ul class="list">
            <li>Investment scams #####</li>
            <li>Phishing attempts #####</li>
            <li>#####</li>
          </ul>
        </div>
      </section>

      <!-- Bottom row: map placeholder + three mini cards -->
      <section class="bottom-grid">
        <div class="map-card">[ Map Placeholder ]</div>
      
        <div class="mini-card">Age Groups</div>
        <div class="mini-card">Scams by Type</div>
      </section>
    </div>
  </div>
</template>

<style scoped>
/* Page wrapper */
.dashboard-page {
  min-height: 100vh;
  background: #f7f7fb;
  padding: 24px 12px;
}
.wrap {
  max-width: 1240px;
  margin: 0 auto;
}

/* State selector grid */
.state-selector {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(72px, 1fr));
  gap: 14px;
  align-items: center;
  margin-bottom: 16px;
}
.state-btn {
  height: 64px;
  border-radius: 999px;
  border: none;
  color: #fff;
  font-weight: 700;
  cursor: pointer;
  box-shadow: 0 6px 16px rgba(0,0,0,.12);
}
.act { background:#3b82f6; }
.nsw { background:#b91c1c; }
.nt  { background:#ea580c; }
.qld { background:#f59e0b; }
.sa  { background:#ef4444; }
.vic { background:#6366f1; }
.wa  { background:#f59e0b; }
.tas { background:#10b981; }

/* Breaking news bar */
.breaking-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
  margin: 10px 0 22px;
}
.breaking-row span {
  background:#ef4444;
  color:#fff;
  font-weight: 800;
  padding: 8px 14px;
  border-radius: 6px;
  box-shadow: 0 6px 16px rgba(239,68,68,.35);
}

/* Top row: 3-column layout */
.top-row-grid {
  display: grid;
  grid-template-columns: 1fr 1.4fr 1fr;
  gap: 18px;
  align-items: stretch;
}

/* Card styles */
.card, .mini-card, .map-card {
  background: #4f86ff;
  color: #fff;
  border-radius: 14px;
  padding: 20px;
  box-shadow: 0 10px 24px rgba(0,0,0,.18);
}
.card h3 { margin: 6px 0 8px; font-size: 1.1rem; font-weight: 800; }
.card .number { font-size: 2.4rem; font-weight: 800; margin-top: 16px; }
.card .list { padding-left: 18px; line-height: 1.6; }
.card .center { text-align: center; }
.card .subt { opacity: .95; margin-bottom: 8px; }

.card.big {
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 220px;
}
.chart-placeholder {
  margin: 14px auto 0;
  width: 88%;
  height: 120px;
  border-radius: 999px;
  background: rgba(255,255,255,.15);
  display: grid;
  place-items: center;
  font-weight: 700;
  letter-spacing: .5px;
}

/* Bottom grid: map spans two columns */
.bottom-grid {
  margin-top: 18px;
  display: grid;
  gap: 16px;
  grid-template-columns: repeat(2, 1fr);
}
.mini-card {
  min-height: 120px;
  display: grid;
  place-items: center;
  font-weight: 800;
  font-size: 1.05rem;
}
.map-card {
  grid-column: span 2;
  min-height: 240px;   /* larger area for future map */
  display: grid;
  place-items: center;
  font-weight: 800;
  font-size: 1.1rem;
}

/* Responsive breakpoints */
@media (min-width: 768px) {
  .bottom-grid { grid-template-columns: repeat(3, 1fr); }
  .map-card { grid-column: span 2; }
}
@media (min-width: 1100px) {
  .bottom-grid { grid-template-columns: repeat(4, 1fr); }
  .map-card { grid-column: span 2; }
}
@media (max-width: 900px) {
  .top-row-grid { grid-template-columns: 1fr; }
}
</style>
