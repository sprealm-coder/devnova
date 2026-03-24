<template>
  <div class="about">
    <div class="hero-section">
      <div class="logo-big">✦</div>
      <h1 class="gradient-text">DevNova</h1>
      <p class="tagline">开发者新星 - 技术资源导航平台</p>
    </div>

    <div class="about-content">
      <div class="card">
        <h3><span class="icon">🎯</span>我们的使命</h3>
        <p>汇聚全球优质技术资源，帮助开发者快速找到所需工具、框架和文档，点亮编程之路。</p>
      </div>

      <div class="card">
        <h3><span class="icon">✨</span>特色功能</h3>
        <div class="features-grid">
          <div class="feature-item">
            <span class="feature-icon">📦</span>
            <span>100+ 精选资源</span>
          </div>
          <div class="feature-item">
            <span class="feature-icon">🏷️</span>
            <span>10 大分类</span>
          </div>
          <div class="feature-item">
            <span class="feature-icon">🔍</span>
            <span>智能搜索</span>
          </div>
          <div class="feature-item">
            <span class="feature-icon">📱</span>
            <span>响应式设计</span>
          </div>
        </div>
      </div>

      <div class="card">
        <h3><span class="icon">🛠️</span>技术栈</h3>
        <div class="tech-list">
          <span class="tech">Vue 3</span>
          <span class="tech">Vite</span>
          <span class="tech">Vue Router</span>
          <span class="tech">Neon UI</span>
        </div>
      </div>

      <div class="card stats-card">
        <div class="stat-item">
          <span class="stat-value">100+</span>
          <span class="stat-label">收录资源</span>
        </div>
        <div class="stat-item">
          <span class="stat-value">10</span>
          <span class="stat-label">分类目录</span>
        </div>
        <div class="stat-item">
          <span class="stat-value">∞</span>
          <span class="stat-label">探索可能</span>
        </div>
      </div>
    </div>

    <footer class="about-footer">
      <p>✦ DevNova · 开发者新星</p>
      <p class="sub">探索技术，发现未来</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'AboutView'
}
</script>

<style scoped>
.about {
  min-height: 100vh;
  padding: 2rem;
}

.hero-section {
  text-align: center;
  padding: 3rem 0;
}

.logo-big {
  font-size: 5rem;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #EC4899, #A855F7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 0 20px rgba(236, 72, 153, 0.5));
}

.gradient-text {
  font-size: 3rem;
  font-weight: 700;
  background: linear-gradient(135deg, #EC4899, #A855F7, #6366F1);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 0.5rem;
}

.tagline {
  color: #94A3B8;
  font-size: 1.1rem;
}

.about-content {
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.card {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 1rem;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.card:hover {
  border-color: rgba(236, 72, 153, 0.3);
  box-shadow: 0 0 30px rgba(236, 72, 153, 0.1);
}

.card h3 {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.2rem;
  color: #fff;
  margin-bottom: 1rem;
}

.icon {
  color: #EC4899;
}

.card p {
  color: #94A3B8;
  line-height: 1.6;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #94A3B8;
}

.feature-icon {
  font-size: 1.2rem;
}

.tech-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech {
  padding: 0.4rem 0.8rem;
  background: rgba(236, 72, 153, 0.1);
  border: 1px solid rgba(236, 72, 153, 0.3);
  color: #EC4899;
  border-radius: 9999px;
  font-size: 0.85rem;
  font-weight: 500;
}

.stats-card {
  display: flex;
  justify-content: space-around;
  text-align: center;
}

.stat-item {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.stat-value {
  font-size: 1.8rem;
  font-weight: 700;
  background: linear-gradient(135deg, #EC4899, #A855F7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.stat-label {
  color: #64748B;
  font-size: 0.85rem;
}

.about-footer {
  text-align: center;
  padding: 3rem 0 1rem;
  color: #64748B;
}

.about-footer .sub {
  font-size: 0.9rem;
  margin-top: 0.5rem;
}

@media (max-width: 768px) {
  .gradient-text { font-size: 2rem; }
  .features-grid { grid-template-columns: 1fr; }
  .stats-card { flex-direction: column; gap: 1rem; }
}
</style>