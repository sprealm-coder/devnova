<template>
  <div class="app">
    <!-- 背景光效 -->
    <div class="glow-bg"></div>
    
    <header class="header">
      <div class="header-content">
        <div class="logo">
          <span class="logo-icon">✦</span>
          <h1>DevNova</h1>
        </div>
        <nav class="nav">
          <router-link to="/" exact-active-class="active">首页</router-link>
          <router-link to="/about" exact-active-class="active">关于</router-link>
        </nav>
      </div>
    </header>
    
    <main>
      <router-view/>
    </main>
    
    <footer class="footer">
      <p>✦ DevNova · 开发者新星</p>
    </footer>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background: #0a0a0f;
  color: #fff;
  min-height: 100vh;
  line-height: 1.6;
  overflow-x: hidden;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
}

/* 背景光效 */
.glow-bg {
  position: fixed;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: 
    radial-gradient(circle at 20% 30%, rgba(168, 85, 247, 0.15) 0%, transparent 40%),
    radial-gradient(circle at 80% 70%, rgba(236, 72, 153, 0.1) 0%, transparent 40%),
    radial-gradient(circle at 50% 50%, rgba(99, 102, 241, 0.08) 0%, transparent 50%);
  pointer-events: none;
  z-index: 0;
  animation: pulse 8s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.1); opacity: 0.8; }
}

/* Header */
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  background: rgba(10, 10, 15, 0.8);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.header-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.logo-icon {
  font-size: 1.5rem;
  background: linear-gradient(135deg, #EC4899, #A855F7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 0 10px rgba(236, 72, 153, 0.5));
}

.logo h1 {
  font-size: 1.5rem;
  font-weight: 700;
  background: linear-gradient(90deg, #fff 0%, #E2E8F0 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav {
  display: flex;
  gap: 0.5rem;
}

.nav a {
  color: #94A3B8;
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 9999px;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s ease;
  border: 1px solid transparent;
}

.nav a:hover {
  color: #fff;
  background: rgba(255, 255, 255, 0.05);
}

.nav a.active {
  color: #fff;
  background: linear-gradient(135deg, rgba(236, 72, 153, 0.2), rgba(168, 85, 247, 0.2));
  border-color: rgba(236, 72, 153, 0.3);
  box-shadow: 0 0 20px rgba(236, 72, 153, 0.2);
}

/* Main */
main {
  flex: 1;
  padding-top: 80px;
  position: relative;
  z-index: 1;
}

/* Footer */
.footer {
  text-align: center;
  padding: 2rem;
  color: #64748B;
  font-size: 0.9rem;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
  position: relative;
  z-index: 1;
}

@media (max-width: 768px) {
  .header-content {
    padding: 1rem;
  }
  
  .logo h1 {
    font-size: 1.25rem;
  }
}
</style>