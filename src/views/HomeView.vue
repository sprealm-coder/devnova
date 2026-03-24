<template>
  <div class="home">
    <!-- 旋转星球背景 -->
    <div class="planet-container">
      <div class="planet">
        <div class="planet-surface">
          <div class="bump b1"></div>
          <div class="bump b2"></div>
          <div class="bump b3"></div>
          <div class="bump b4"></div>
          <div class="bump b5"></div>
          <div class="bump b6"></div>
          <div class="bump b7"></div>
          <div class="bump b8"></div>
          <div class="bump b9"></div>
          <div class="bump b10"></div>
          <div class="bump b11"></div>
          <div class="bump b12"></div>
        </div>
      </div>
    </div>
    
    <section class="hero">
      <div class="hero-content">
        <div class="badge"><span class="badge-dot"></span>收录 100+ 优质资源</div>
        <h1 class="hero-title">探索<span class="gradient-text">开发者</span>的<br>新星世界</h1>
        <p class="hero-subtitle">发现前沿技术资源，点亮你的编程之路</p>
        <div class="search-box">
          <span class="search-icon">🔍</span>
          <input v-model="searchQuery" placeholder="搜索资源、工具、框架..." @keyup.enter="handleSearch">
        </div>
        <div class="stats">
          <div class="stat-card"><span class="stat-number">100+</span><span class="stat-label">精选资源</span></div>
          <div class="stat-card"><span class="stat-number">10</span><span class="stat-label">分类目录</span></div>
          <div class="stat-card"><span class="stat-number">∞</span><span class="stat-label">探索可能</span></div>
        </div>
      </div>
    </section>

    <nav class="category-nav">
      <button v-for="cat in categories" :key="cat.id" :class="['cat-btn', { active: activeCategory === cat.id }]" @click="activeCategory = cat.id">
        <span class="cat-icon">{{ cat.icon }}</span>{{ cat.name }}
      </button>
    </nav>

    <div class="content">
      <section v-if="shouldShow('featured')" class="section">
        <div class="section-header"><h2><span class="section-icon">✦</span>精选推荐</h2><span class="section-desc">编辑精选的优质资源</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(featuredItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header">
                <img :src="item.favicon" class="favicon" onerror="this.style.display='none'">
                <h3>{{ item.title }}</h3>
                <span v-if="item.hot" class="hot-badge">HOT</span>
              </div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('frontend')" class="section">
        <div class="section-header"><h2><span class="section-icon">⚡</span>前端开发</h2><span class="section-desc">现代前端框架与工具</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(frontendItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('backend')" class="section">
        <div class="section-header"><h2><span class="section-icon">🔧</span>后端开发</h2><span class="section-desc">服务端技术与基础设施</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(backendItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('ai')" class="section">
        <div class="section-header"><h2><span class="section-icon">🤖</span>AI 编程</h2><span class="section-desc">人工智能辅助开发工具</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(aiItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3><span v-if="item.new" class="new-badge">NEW</span></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('design')" class="section">
        <div class="section-header"><h2><span class="section-icon">🎨</span>设计资源</h2><span class="section-desc">UI/UX 设计工具与灵感</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(designItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('tools')" class="section">
        <div class="section-header"><h2><span class="section-icon">🛠️</span>开发工具</h2><span class="section-desc">提升效率的实用工具</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(toolsItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('docs')" class="section">
        <div class="section-header"><h2><span class="section-icon">📚</span>技术文档</h2><span class="section-desc">官方文档与学习资源</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(docsItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('community')" class="section">
        <div class="section-header"><h2><span class="section-icon">👥</span>技术社区</h2><span class="section-desc">开发者交流与讨论</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(communityItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <section v-if="shouldShow('opensource')" class="section">
        <div class="section-header"><h2><span class="section-icon">⭐</span>开源项目</h2><span class="section-desc">GitHub 热门开源项目</span></div>
        <div class="cards-grid">
          <a v-for="item in filterItems(opensourceItems)" :key="item.id" :href="item.url" target="_blank" class="resource-card">
            <div class="card-glow"></div>
            <div class="card-content">
              <div class="card-header"><img :src="item.favicon" class="favicon" onerror="this.style.display='none'"><h3>{{ item.title }}</h3><span v-if="item.stars" class="star-badge">⭐ {{ item.stars }}</span></div>
              <p class="card-desc">{{ item.description }}</p>
              <div class="card-tags"><span v-for="tag in item.tags" :key="tag" class="tag">{{ tag }}</span></div>
            </div>
          </a>
        </div>
      </section>

      <div v-if="searchQuery && !hasSearchResults" class="empty-state">
        <div class="empty-icon">🔍</div>
        <p>未找到 "{{ searchQuery }}" 相关内容</p>
        <button @click="searchQuery = ''" class="clear-btn">清除搜索</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      searchQuery: '',
      activeCategory: 'all',
      categories: [
        { id: 'all', name: '全部', icon: '◈' },
        { id: 'featured', name: '精选', icon: '✦' },
        { id: 'frontend', name: '前端', icon: '⚡' },
        { id: 'backend', name: '后端', icon: '🔧' },
        { id: 'ai', name: 'AI', icon: '◉' },
        { id: 'design', name: '设计', icon: '◉' },
        { id: 'tools', name: '工具', icon: '◆' },
        { id: 'docs', name: '文档', icon: '◎' },
        { id: 'community', name: '社区', icon: '◇' },
        { id: 'opensource', name: '开源', icon: '★' }
      ],
      featuredItems: [
        { id: 1, title: 'GitHub', description: '全球最大的代码托管平台', url: 'https://github.com', favicon: 'https://github.com/favicon.ico', tags: ['代码托管', '开源'], hot: true },
        { id: 2, title: 'Stack Overflow', description: '程序员问答社区', url: 'https://stackoverflow.com', favicon: 'https://stackoverflow.com/favicon.ico', tags: ['问答', '社区'], hot: true },
        { id: 3, title: 'MDN Web Docs', description: 'Web 开发权威文档', url: 'https://developer.mozilla.org', favicon: 'https://developer.mozilla.org/favicon.ico', tags: ['文档', '参考'], hot: true },
        { id: 4, title: 'Vercel', description: '前端部署平台', url: 'https://vercel.com', favicon: 'https://vercel.com/favicon.ico', tags: ['部署', 'Serverless'], hot: true },
        { id: 5, title: 'Figma', description: '协作界面设计工具', url: 'https://figma.com', favicon: 'https://figma.com/favicon.ico', tags: ['设计', 'UI'], hot: true },
        { id: 6, title: 'ChatGPT', description: 'AI 对话与编程助手', url: 'https://chat.openai.com', favicon: 'https://chat.openai.com/favicon.ico', tags: ['AI', '编程'], hot: true }
      ],
      frontendItems: [
        { id: 101, title: 'Vue.js', description: '渐进式 JavaScript 框架', url: 'https://vuejs.org', favicon: 'https://vuejs.org/logo.svg', tags: ['框架', 'Vue'] },
        { id: 102, title: 'React', description: '用于构建用户界面的库', url: 'https://react.dev', favicon: 'https://react.dev/favicon.ico', tags: ['框架', 'React'] },
        { id: 103, title: 'Angular', description: 'Google 前端框架', url: 'https://angular.io', favicon: 'https://angular.io/favicon.ico', tags: ['框架', 'Angular'] },
        { id: 104, title: 'Svelte', description: '编译时框架', url: 'https://svelte.dev', favicon: 'https://svelte.dev/favicon.png', tags: ['框架', 'Svelte'] },
        { id: 105, title: 'Tailwind CSS', description: '原子化 CSS 框架', url: 'https://tailwindcss.com', favicon: 'https://tailwindcss.com/favicon.ico', tags: ['CSS', 'UI'] },
        { id: 106, title: 'Next.js', description: 'React 全栈框架', url: 'https://nextjs.org', favicon: 'https://nextjs.org/favicon.ico', tags: ['框架', 'React', 'SSR'] },
        { id: 107, title: 'TypeScript', description: 'JavaScript 超集', url: 'https://typescriptlang.org', favicon: 'https://typescriptlang.org/favicon.ico', tags: ['语言', '类型'] },
        { id: 108, title: 'Vite', description: '下一代构建工具', url: 'https://vitejs.dev', favicon: 'https://vitejs.dev/logo.svg', tags: ['构建工具', '快速'] }
      ],
      backendItems: [
        { id: 201, title: 'Node.js', description: 'JavaScript 运行时', url: 'https://nodejs.org', favicon: 'https://nodejs.org/favicon.ico', tags: ['运行时', 'JavaScript'] },
        { id: 202, title: 'Spring Boot', description: 'Java 微服务框架', url: 'https://spring.io', favicon: 'https://spring.io/favicon.ico', tags: ['框架', 'Java'] },
        { id: 203, title: 'FastAPI', description: '高性能 Python API 框架', url: 'https://fastapi.tiangolo.com', favicon: 'https://fastapi.tiangolo.com/img/favicon.png', tags: ['框架', 'Python'] },
        { id: 204, title: 'PostgreSQL', description: '开源关系型数据库', url: 'https://postgresql.org', favicon: 'https://postgresql.org/favicon.ico', tags: ['数据库', 'SQL'] },
        { id: 205, title: 'MongoDB', description: '文档型 NoSQL 数据库', url: 'https://mongodb.com', favicon: 'https://mongodb.com/favicon.ico', tags: ['数据库', 'NoSQL'] },
        { id: 206, title: 'Redis', description: '内存数据结构存储', url: 'https://redis.io', favicon: 'https://redis.io/favicon.ico', tags: ['缓存', 'NoSQL'] },
        { id: 207, title: 'Docker', description: '容器化平台', url: 'https://docker.com', favicon: 'https://docker.com/favicon.ico', tags: ['容器', 'DevOps'] },
        { id: 208, title: 'Kubernetes', description: '容器编排系统', url: 'https://kubernetes.io', favicon: 'https://kubernetes.io/favicon.ico', tags: ['容器', '编排'] }
      ],
      aiItems: [
        { id: 301, title: 'ChatGPT', description: 'OpenAI 对话模型', url: 'https://chat.openai.com', favicon: 'https://chat.openai.com/favicon.ico', tags: ['AI', '对话'], new: true },
        { id: 302, title: 'Claude', description: 'Anthropic AI 助手', url: 'https://claude.ai', favicon: 'https://claude.ai/favicon.ico', tags: ['AI', '编程'], new: true },
        { id: 303, title: 'GitHub Copilot', description: 'AI 代码补全', url: 'https://github.com/features/copilot', favicon: 'https://github.com/favicon.ico', tags: ['AI', 'IDE'] },
        { id: 304, title: 'Cursor', description: 'AI 代码编辑器', url: 'https://cursor.sh', favicon: 'https://cursor.sh/favicon.ico', tags: ['AI', '编辑器'], new: true },
        { id: 305, title: 'V0', description: 'AI 生成 UI', url: 'https://v0.dev', favicon: 'https://v0.dev/favicon.ico', tags: ['AI', 'UI生成'], new: true },
        { id: 306, title: 'Ollama', description: '本地运行大模型', url: 'https://ollama.com', favicon: 'https://ollama.com/favicon.ico', tags: ['AI', '本地'], new: true }
      ],
      designItems: [
        { id: 401, title: 'Figma', description: '协作设计工具', url: 'https://figma.com', favicon: 'https://figma.com/favicon.ico', tags: ['设计', 'UI'] },
        { id: 402, title: 'Dribbble', description: '设计灵感社区', url: 'https://dribbble.com', favicon: 'https://dribbble.com/favicon.ico', tags: ['灵感', '社区'] },
        { id: 403, title: 'Coolors', description: '配色方案生成', url: 'https://coolors.co', favicon: 'https://coolors.co/favicon.ico', tags: ['配色', '工具'] },
        { id: 404, title: 'Iconify', description: '开源图标库', url: 'https://iconify.design', favicon: 'https://iconify.design/favicon.ico', tags: ['图标', 'SVG'] },
        { id: 405, title: 'Unsplash', description: '免费高质量图片', url: 'https://unsplash.com', favicon: 'https://unsplash.com/favicon.ico', tags: ['图片', '素材'] }
      ],
      toolsItems: [
        { id: 501, title: 'Postman', description: 'API 测试工具', url: 'https://postman.com', favicon: 'https://postman.com/favicon.ico', tags: ['API', '测试'] },
        { id: 502, title: 'CodeSandbox', description: '在线 IDE', url: 'https://codesandbox.io', favicon: 'https://codesandbox.io/favicon.ico', tags: ['IDE', '在线'] },
        { id: 503, title: 'Regexr', description: '正则表达式测试', url: 'https://regexr.com', favicon: 'https://regexr.com/favicon.ico', tags: ['正则', '测试'] },
        { id: 504, title: 'Carbon', description: '代码截图美化', url: 'https://carbon.now.sh', favicon: 'https://carbon.now.sh/favicon.ico', tags: ['代码', '截图'] },
        { id: 505, title: 'Excalidraw', description: '手绘风格图表', url: 'https://excalidraw.com', favicon: 'https://excalidraw.com/favicon.ico', tags: ['图表', '白板'] }
      ],
      docsItems: [
        { id: 601, title: 'MDN Web Docs', description: 'Web 开发文档', url: 'https://developer.mozilla.org', favicon: 'https://developer.mozilla.org/favicon.ico', tags: ['文档', 'Web'] },
        { id: 602, title: 'DevDocs', description: '离线 API 文档', url: 'https://devdocs.io', favicon: 'https://devdocs.io/favicon.ico', tags: ['文档', 'API'] },
        { id: 603, title: 'LeetCode', description: '算法题库', url: 'https://leetcode.cn', favicon: 'https://leetcode.cn/favicon.ico', tags: ['算法', '面试'] },
        { id: 604, title: 'freeCodeCamp', description: '免费编程学习', url: 'https://chinese.freecodecamp.org', favicon: 'https://chinese.freecodecamp.org/favicon.ico', tags: ['教程', '免费'] }
      ],
      communityItems: [
        { id: 701, title: '掘金', description: '中文技术社区', url: 'https://juejin.cn', favicon: 'https://juejin.cn/favicon.ico', tags: ['社区', '中文'] },
        { id: 702, title: 'V2EX', description: '创意工作者社区', url: 'https://v2ex.com', favicon: 'https://v2ex.com/favicon.ico', tags: ['社区', '技术'] },
        { id: 703, title: 'GitHub', description: '开源代码托管', url: 'https://github.com', favicon: 'https://github.com/favicon.ico', tags: ['代码', '开源'] },
        { id: 704, title: 'Hacker News', description: '技术新闻', url: 'https://news.ycombinator.com', favicon: 'https://news.ycombinator.com/favicon.ico', tags: ['新闻', '技术'] }
      ],
      opensourceItems: [
        { id: 801, title: 'Vue', description: '渐进式 JS 框架', url: 'https://github.com/vuejs/core', favicon: 'https://github.com/favicon.ico', tags: ['开源', 'Vue'], stars: '46k' },
        { id: 802, title: 'React', description: 'UI 库', url: 'https://github.com/facebook/react', favicon: 'https://github.com/favicon.ico', tags: ['开源', 'React'], stars: '230k' },
        { id: 803, title: 'VS Code', description: '代码编辑器', url: 'https://github.com/microsoft/vscode', favicon: 'https://github.com/favicon.ico', tags: ['开源', 'IDE'], stars: '165k' },
        { id: 804, title: 'Awesome', description: '精选资源列表', url: 'https://github.com/sindresorhus/awesome', favicon: 'https://github.com/favicon.ico', tags: ['开源', '资源'], stars: '350k' }
      ]
    }
  },
  computed: {
    totalCount() { return 100 },
    hasSearchResults() {
      const all = [...this.featuredItems, ...this.frontendItems, ...this.backendItems, 
                   ...this.aiItems, ...this.designItems, ...this.toolsItems,
                   ...this.docsItems, ...this.communityItems, ...this.opensourceItems]
      return all.some(item => 
        item.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        item.description.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        item.tags.some(tag => tag.toLowerCase().includes(this.searchQuery.toLowerCase()))
      )
    }
  },
  methods: {
    shouldShow(cat) { return this.activeCategory === 'all' || this.activeCategory === cat },
    filterItems(items) {
      if (!this.searchQuery) return items
      const q = this.searchQuery.toLowerCase()
      return items.filter(item => 
        item.title.toLowerCase().includes(q) ||
        item.description.toLowerCase().includes(q) ||
        item.tags.some(tag => tag.toLowerCase().includes(q))
      )
    },
    handleSearch() { document.querySelector('.content')?.scrollIntoView({ behavior: 'smooth' }) }
  }
}
</script>

<style scoped>
/* 旋转星球 */
.planet-container {
  position: fixed;
  top: 50%;
  right: -200px;
  transform: translateY(-50%);
  width: 600px;
  height: 600px;
  z-index: 0;
  pointer-events: none;
}

.planet {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background: linear-gradient(135deg, #EC4899 0%, #A855F7 50%, #6366F1 100%);
  position: relative;
  animation: rotate 60s linear infinite;
  box-shadow: 
    0 0 100px rgba(236, 72, 153, 0.5),
    0 0 200px rgba(168, 85, 247, 0.3),
    inset -50px -50px 100px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.planet-surface {
  width: 100%;
  height: 100%;
  position: relative;
}

.bump {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.4), rgba(255, 255, 255, 0.1));
  box-shadow: 
    inset 2px 2px 5px rgba(255, 255, 255, 0.5),
    inset -2px -2px 5px rgba(0, 0, 0, 0.2),
    0 5px 15px rgba(0, 0, 0, 0.2);
}

.b1 { width: 80px; height: 80px; top: 10%; left: 20%; }
.b2 { width: 60px; height: 60px; top: 25%; left: 60%; }
.b3 { width: 100px; height: 100px; top: 40%; left: 10%; }
.b4 { width: 50px; height: 50px; top: 15%; left: 75%; }
.b5 { width: 70px; height: 70px; top: 55%; left: 70%; }
.b6 { width: 90px; height: 90px; top: 65%; left: 25%; }
.b7 { width: 45px; height: 45px; top: 75%; left: 60%; }
.b8 { width: 65px; height: 65px; top: 30%; left: 35%; }
.b9 { width: 55px; height: 55px; top: 50%; left: 45%; }
.b10 { width: 85px; height: 85px; top: 80%; left: 40%; }
.b11 { width: 40px; height: 40px; top: 5%; left: 50%; }
.b12 { width: 75px; height: 75px; top: 60%; left: 5%; }

.home { min-height: 100vh; position: relative; }
.hero { padding: 4rem 2rem 3rem; text-align: center; position: relative; z-index: 1; }
.hero-content { max-width: 800px; margin: 0 auto; }
.badge { display: inline-flex; align-items: center; gap: 0.5rem; padding: 0.5rem 1rem; background: rgba(236, 72, 153, 0.1); border: 1px solid rgba(236, 72, 153, 0.3); border-radius: 9999px; color: #EC4899; font-size: 0.85rem; font-weight: 500; margin-bottom: 1.5rem; }
.badge-dot { width: 8px; height: 8px; background: #EC4899; border-radius: 50%; animation: pulse 2s infinite; }
@keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
.hero-title { font-size: 3.5rem; font-weight: 700; line-height: 1.2; margin-bottom: 1rem; color: #fff; }
.gradient-text { background: linear-gradient(135deg, #EC4899, #A855F7, #6366F1); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.hero-subtitle { font-size: 1.25rem; color: #94A3B8; margin-bottom: 2rem; }
.search-box { max-width: 500px; margin: 0 auto 2rem; position: relative; }
.search-box input { width: 100%; padding: 1rem 1rem 1rem 3rem; background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 9999px; color: #fff; font-size: 1rem; outline: none; transition: all 0.3s; }
.search-box input:focus { border-color: rgba(236, 72, 153, 0.5); box-shadow: 0 0 30px rgba(236, 72, 153, 0.2); }
.search-box input::placeholder { color: #64748B; }
.search-icon { position: absolute; left: 1rem; top: 50%; transform: translateY(-50%); font-size: 1.2rem; }
.stats { display: flex; justify-content: center; gap: 2rem; flex-wrap: wrap; }
.stat-card { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 1rem; padding: 1.5rem 2rem; text-align: center; transition: all 0.3s; }
.stat-card:hover { border-color: rgba(236, 72, 153, 0.3); box-shadow: 0 0 30px rgba(236, 72, 153, 0.1); }
.stat-number { display: block; font-size: 2rem; font-weight: 700; background: linear-gradient(135deg, #EC4899, #A855F7); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.stat-label { color: #64748B; font-size: 0.9rem; }
.category-nav { display: flex; justify-content: center; gap: 0.5rem; padding: 1rem 2rem; flex-wrap: wrap; border-bottom: 1px solid rgba(255, 255, 255, 0.05); }
.cat-btn { display: flex; align-items: center; gap: 0.4rem; padding: 0.6rem 1.2rem; background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 9999px; color: #94A3B8; font-size: 0.9rem; cursor: pointer; transition: all 0.3s; }
.cat-btn:hover { background: rgba(255, 255, 255, 0.08); color: #fff; }
.cat-btn.active { background: linear-gradient(135deg, rgba(236, 72, 153, 0.2), rgba(168, 85, 247, 0.2)); border-color: rgba(236, 72, 153, 0.5); color: #fff; box-shadow: 0 0 20px rgba(236, 72, 153, 0.3); }
.content { max-width: 1400px; margin: 0 auto; padding: 2rem; }
.section { margin-bottom: 3rem; }
.section-header { display: flex; align-items: center; gap: 1rem; margin-bottom: 1.5rem; }
.section-header h2 { display: flex; align-items: center; gap: 0.5rem; font-size: 1.5rem; font-weight: 600; color: #fff; }
.section-icon { color: #EC4899; }
.section-desc { color: #64748B; font-size: 0.9rem; }
.cards-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 1rem; }
.resource-card { position: relative; background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 1rem; padding: 1.5rem; text-decoration: none; color: inherit; transition: all 0.3s; overflow: hidden; }
.resource-card:hover { transform: translateY(-4px); border-color: rgba(236, 72, 153, 0.3); box-shadow: 0 10px 40px rgba(236, 72, 153, 0.15); }
.card-glow { position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: radial-gradient(circle, rgba(236, 72, 153, 0.1) 0%, transparent 70%); opacity: 0; transition: opacity 0.3s; pointer-events: none; }
.resource-card:hover .card-glow { opacity: 1; }
.card-content { position: relative; z-index: 1; }
.card-header { display: flex; align-items: center; gap: 0.75rem; margin-bottom: 0.75rem; }
.favicon { width: 24px; height: 24px; border-radius: 4px; }
.card-header h3 { flex: 1; font-size: 1rem; color: #fff; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.hot-badge { background: linear-gradient(135deg, #EC4899, #F472B6); color: #fff; padding: 0.2rem 0.5rem; border-radius: 9999px; font-size: 0.7rem; font-weight: 600; }
.new-badge { background: linear-gradient(135deg, #10B981, #34D399); color: #fff; padding: 0.2rem 0.5rem; border-radius: 9999px; font-size: 0.7rem; font-weight: 600; }
.star-badge { background: rgba(234, 179, 8, 0.2); color: #EAB308; padding: 0.2rem 0.5rem; border-radius: 9999px; font-size: 0.75rem; }
.card-desc { color: #94A3B8; font-size: 0.85rem; line-height: 1.5; margin-bottom: 1rem; }
.card-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; }
.tag { background: rgba(236, 72, 153, 0.1); color: #EC4899; padding: 0.25rem 0.6rem; border-radius: 9999px; font-size: 0.75rem; }
.empty-state { text-align: center; padding: 4rem; color: #64748B; }
.empty-icon { font-size: 4rem; margin-bottom: 1rem; }
.clear-btn { margin-top: 1rem; padding: 0.75rem 1.5rem; background: linear-gradient(135deg, #EC4899, #A855F7); border: none; border-radius: 9999px; color: #fff; cursor: pointer; font-size: 1rem; }
@media (max-width: 768px) { .hero-title { font-size: 2.5rem; } .cards-grid { grid-template-columns: 1fr; } }
</style>