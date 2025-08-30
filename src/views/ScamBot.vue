<template>
  <div class="scambot-page">
    <!-- header: unchanged -->
    <div class="header-card">
      <h2>🤖 ScamDetector</h2>
      <p>
        Hi! I’m ScamMate, your scam-spotting buddy.<br>
        Paste a suspicious message or upload a screenshot—I’ll flag risks for you.
      </p>
    </div>

    <!-- two-column layout -->
    <div class="risk-grid">
      <!-- left: document card -->
      <section class="card doc-card">
        <div class="doc-toolbar">
          <h3>Untitled document</h3>
          <button class="btn ghost" @click="pasteFromClipboard">Paste text</button>
        </div>

        <textarea
          v-model="userInput"
          class="doc-input"
          placeholder="Paste or type the message here..."
        ></textarea>

        <div class="doc-actions">
          <label class="btn light" for="fileInput">Upload screenshot</label>
          <input id="fileInput" type="file" class="hidden" accept="image/*,text/plain" @change="handleFile">
          <button class="btn primary" @click="analyze">Detect</button>
        </div>
      </section>

      <!-- right: risk card with image -->
      <section class="card gauge-card">
        <p v-if="wordCount < 25" class="hint">Enter at least 25 words to show risk</p>

        <div class="gauge-wrap">
          <img class="meter-img" src="/risk-meter.png" alt="Risk meter" />
          <div class="risk-text" :class="riskLevelClass">{{ riskLevel }}</div>
          <div class="chip">
            <span class="dot">!</span>
            {{ likelihoodLabel }}
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"

const userInput = ref("")
const score = ref(0) // 0–100

const wordCount = computed(() =>
  userInput.value.trim().split(/\s+/).filter(Boolean).length
)

function analyze() {
  if (wordCount.value < 25) {
    score.value = 0
    return
  }
  const text = userInput.value.toLowerCase()

  const keywords = [
    'verify','click','urgent','immediately','locked','password',
    'social security','ssn','bank','transfer','gift','win','prize','link',
    'confirm','account','update','address','login','suspend'
  ]
  let s = 15
  keywords.forEach(k => { if (text.includes(k)) s += 6 })

  if (/(https?:\/\/)?[^\s]+\.(ru|tk|top|xyz|click|zip|mov|live|icu|work)/.test(text)) s += 25
  if (/http|www\./.test(text)) s += 10
  if (/(full name|date of birth|dob|ssn|id|passport|credit card|cvv)/.test(text)) s += 25

  score.value = Math.max(0, Math.min(100, s))
}

const riskLevel = computed(() => {
  if (score.value >= 70) return 'High'
  if (score.value >= 40) return 'Medium'
  return 'Low'
})
const riskLevelClass = computed(() => riskLevel.value.toLowerCase())
const likelihoodLabel = computed(() => (score.value >= 40 ? 'Likely' : 'Unlikely'))

async function pasteFromClipboard() {
  try {
    const txt = await navigator.clipboard.readText()
    if (txt) userInput.value = txt
  } catch (e) {
    console.warn('Clipboard not available', e)
  }
}

function handleFile(e) {
  const file = e.target.files?.[0]
  if (file) {
    userInput.value += (userInput.value ? '\n\n' : '') + `[Uploaded file: ${file.name}]`
  }
}
</script>

<style scoped>
/* page */
.scambot-page {
  background: #f3e8ff;
  min-height: 100vh;
  padding: 20px;
  font-size: 1rem;
}

/* header */
.header-card {
  background: #7c3aed;
  color: white;
  text-align: center;
  padding: 24px 16px;
  border-radius: 12px;
  margin-bottom: 20px;
}
.header-card h2 { font-size: 1.8rem; margin-bottom: 10px; }
.header-card p  { font-size: 1rem; line-height: 1.6; }
@media (min-width: 768px) {
  .header-card h2 { font-size: 2.4rem; }
  .header-card p  { font-size: 1.3rem; }
}

/* grid */
.risk-grid {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  gap: 20px;
  grid-template-columns: 1fr;
}
@media (min-width: 960px) {
  .risk-grid { grid-template-columns: 1.2fr 1fr; }
}

/* cards */
.card {
  background: #ffffff;
  border-radius: 14px;
  padding: 18px;
  box-shadow: 0 12px 28px rgba(17, 24, 39, .12);
}
.doc-card { overflow: hidden; }            /* fix: keep children inside rounded card */

/* left card */
.doc-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}
.doc-toolbar h3 { margin: 0; font-size: 1.1rem; color: #111827; }
.doc-input {
  width: 100%;
  min-height: 260px;
  border: 0;
  outline: 0;
  resize: vertical;
  border-radius: 10px;
  background: #ffeef0;
  padding: 16px;
  font-size: 1rem;
  line-height: 1.6;
  color: #1f2937;
  box-sizing: border-box;                  /* fix: prevent overflow from padding */
}
.doc-actions {
  display: flex;
  gap: 12px;
  justify-content: flex-end;
  margin-top: 12px;
}
.hidden { display: none; }

/* buttons */
.btn {
  border: 0;
  border-radius: 10px;
  padding: 10px 14px;
  font-weight: 700;
  cursor: pointer;
}
.btn.primary {
  background: #7c3aed;
  color: #fff;
  box-shadow: 0 8px 18px rgba(124, 58, 237, .35);
}
.btn.primary:hover { filter: brightness(1.05); }
.btn.light { background: #f3f4f6; color: #374151; }
.btn.ghost { background: #e9d5ff; color: #5b21b6; }

/* right card */
.hint {
  text-align: center;
  color: #6b7280;
  font-weight: 600;
  margin: 8px 0 12px;
}
.gauge-wrap {
  display: grid;
  place-items: center;
  gap: 10px;
}
.meter-img {
  width: 100%;
  max-width: 420px;
  height: auto;
  display: block;
  border-radius: 8px;
}
.risk-text { font-size: 1.8rem; font-weight: 800; }
.risk-text.low    { color: #16a34a; }
.risk-text.medium { color: #f59e0b; }
.risk-text.high   { color: #ef4444; }

.chip {
  background: #eef2ff;
  color: #111827;
  font-weight: 700;
  padding: 8px 12px;
  border-radius: 999px;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}
.chip .dot {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background: #111827;
  color: #fff;
  display: grid;
  place-items: center;
  font-size: .9rem;
}
</style>
