<template>
  <header class="navbar-header">
    <div class="navbar-container">
      <!-- 左侧 logo 和品牌名 -->
      <div class="navbar-left">
        <img src="../assets/logo.png" alt="CyberMate logo" class="logo" />
        <span class="brand">CyberMate</span>
      </div>

      <!-- 右侧导航 -->
      <nav class="navbar-nav">
        <router-link to="/">Home</router-link>
        <router-link to="/dashboard">Dashboard</router-link>
        <router-link to="/scambot">ScamBot</router-link>
        <router-link to="/riskscore">Risk Score</router-link>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.navbar-header {
  background: #3b1d74; /* 深紫色背景 */
  padding: 0;
  position: relative;
  z-index: 1000; /* 让导航永远在最上层 */
}

.navbar-container {
  max-width: 1300px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  padding: 16px 32px;
  justify-content: space-between;
}

.navbar-left {
  display: flex;
  align-items: center;
}

.logo {
  width: 40px;
  height: 40px;
  margin-right: 10px;
}

.brand {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin-right: 24px;
  font-family: 'Segoe UI', sans-serif;
}

.navbar-nav {
  display: flex;
  gap: 32px;
}

.navbar-nav a {
  font-size: 1.4rem;
  color: #ffffff;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s;
}

.navbar-nav a:hover {
  color: #60a5fa; /* hover 变蓝 */
  text-decoration: underline;
}

.navbar-nav a.router-link-active {
  color: #60a5fa; /* 当前路由高亮 */
  font-weight: bold;
}
</style>
