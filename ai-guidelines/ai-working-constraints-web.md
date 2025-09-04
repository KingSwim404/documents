# [项目名称] - Web项目AI工作约束

> **模板使用说明**
> 
> 本文档是Web项目AI约束模板，使用前请：
> 1. 替换 `[项目名称]` 为实际项目名称
> 2. 替换 `[技术栈]` 为实际使用的技术栈
> 3. 根据项目需求调整技术约束
> 4. 删除本使用说明部分
> 
> **必需替换的占位符**：
> - `[项目名称]` → 你的项目名称
> - `[技术栈]` → 实际技术栈（如React、Vue、Angular等）
> - `[部署域名]` → 实际部署域名
> - `[开发端口]` → 开发服务器端口

## 文档目的

本文档记录AI助手在 **[项目名称]** Web项目开发过程中必须遵守的约束和规范，适用于Web前端项目，包括静态站点、SPA应用、PWA等。这些约束基于Web开发的最佳实践和常见问题总结而成。

## 🌐 Web项目通用约束

### 1. 静态站点构建规范

**构建产物组织原则**：
- **清晰的目录结构**：HTML文件和资源文件分离
- **资源集中管理**：CSS、JS、图片等资源统一组织
- **缓存友好**：文件名包含hash，支持长期缓存
- **部署兼容**：考虑不同部署环境的路径要求

**推荐构建结构**：
```
dist/
├── index.html              # 主页面
├── assets/                 # 资源目录（推荐）
│   ├── css/               # 样式文件
│   ├── js/                # JavaScript文件
│   └── images/            # 图片资源
├── static/                 # 静态文件（备选）
└── [必要的根目录文件]      # 如manifest.json、robots.txt
```

### 2. 部署环境适配

**通用部署考虑**：
- **路径配置**：支持子目录部署和根目录部署
- **静态文件服务**：确保所有资源可正确访问
- **SPA路由支持**：配置服务器支持前端路由
- **HTTPS支持**：现代Web应用的基本要求

**路径处理最佳实践**：
```javascript
// ✅ 推荐：使用相对路径或配置化路径
const basePath = process.env.PUBLIC_URL || '';
const imagePath = `${basePath}/images/logo.png`;

// ✅ 推荐：构建工具处理路径
import logoUrl from './assets/logo.png';

// ❌ 避免：硬编码绝对路径
const imagePath = '/static/images/logo.png';
```

### 3. 前端技术栈选择原则

**框架选择考虑因素**：
- **项目需求匹配**：框架特性与项目需求的契合度
- **技术熟悉度**：团队对技术栈的掌握程度
- **生态系统成熟度**：社区支持、插件生态、文档完善度
- **长期维护性**：技术栈的发展前景和稳定性

**常见技术栈适用场景**：
- **静态站点**：[技术栈] + 静态生成器
- **SPA应用**：[技术栈] + 路由管理
- **SSR应用**：[技术栈] + 服务端渲染
- **PWA应用**：支持Service Worker的现代框架

**技术选择最佳实践**：
- ✅ 选择成熟稳定的技术栈
- ✅ 考虑项目的长期维护需求
- ✅ 评估学习成本和开发效率
- ❌ 避免过度追求新技术
- ❌ 避免技术栈过于复杂

## 📱 响应式设计约束

### 移动端适配要求

**设计原则**：
- **移动优先**：优先考虑移动端体验
- **渐进增强**：从移动端向桌面端扩展
- **触摸友好**：按钮和链接适合触摸操作
- **性能优化**：考虑移动端网络和性能限制

**技术实现**：
- 使用响应式CSS（Flexbox、Grid）
- 合理的断点设置
- 图片和媒体资源优化
- 字体大小和行高适配

### 浏览器兼容性

**兼容性要求**：
- **现代浏览器**：Chrome、Firefox、Safari、Edge 最新版本
- **移动浏览器**：iOS Safari、Android Chrome
- **降级策略**：为不支持的功能提供备用方案

**代码质量标准**：
```typescript
// ✅ 正确做法：提供兼容性检查和降级
try {
  // 使用现代API
  if ('IntersectionObserver' in window) {
    const observer = new IntersectionObserver(callback);
  } else {
    // 降级到传统方案
    fallbackScrollHandler();
  }
} catch (error) {
  console.warn('Feature not supported, using fallback');
  fallbackMethod();
}

// ❌ 错误做法：直接使用可能不支持的API
const observer = new IntersectionObserver(callback);
```

## 🎨 UI/UX 开发约束

### 主题和样式系统

**主题色约束**：
> **定制说明**：根据项目设计规范调整主题色

- **主色调**：使用项目指定的主题色
- **色彩系统**：建立完整的色彩变量系统
- **暗色模式**：考虑暗色模式支持（如果需要）

**CSS组织原则**：
```css
/* ✅ 推荐：使用CSS变量 */
:root {
  --primary-color: #[主题色];
  --primary-hover: #[主题色悬停];
  --text-color: #333;
}

.button {
  background-color: var(--primary-color);
  color: var(--text-color);
}

/* ❌ 避免：硬编码颜色值 */
.button {
  background-color: #0ABAB5;
  color: #333;
}
```

### 交互体验约束

**用户体验原则**：
- **加载状态**：提供明确的加载反馈
- **错误处理**：友好的错误提示和恢复机制
- **无障碍访问**：支持键盘导航和屏幕阅读器
- **性能感知**：优化首屏加载时间

## 📦 资源管理约束

### 静态资源处理

**图片资源**：
- **格式选择**：优先使用 WebP，提供 JPEG/PNG 降级
- **尺寸优化**：提供多种尺寸适配不同设备
- **懒加载**：非关键图片实现懒加载
- **CDN支持**：考虑CDN部署的路径要求

**字体资源**：
- **Web字体**：使用 `font-display: swap` 优化加载
- **字体降级**：提供系统字体降级方案
- **字体子集**：只加载需要的字符集

### 代码分割和优化

**JavaScript优化**：
```javascript
// ✅ 推荐：动态导入和代码分割
const LazyComponent = lazy(() => import('./LazyComponent'));

// 路由级别的代码分割
const routes = [
  {
    path: '/[路由路径]',
    component: () => import('./pages/[页面组件].vue')
  }
];

// ❌ 避免：全量导入大型库
import * as _ from 'lodash';

// ✅ 推荐：按需导入
import { debounce } from 'lodash-es';
```

## 🔧 开发工具和流程约束

### 构建工具配置

**[技术栈] 配置最佳实践**：
> **定制说明**：根据实际使用的构建工具调整配置

```typescript
// 示例：Vite配置
export default defineConfig({
  base: '[部署路径]',
  build: {
    rollupOptions: {
      output: {
        // 资源文件统一放入assets目录
        assetFileNames: 'assets/[name]-[hash][extname]',
        chunkFileNames: 'assets/[name]-[hash].js',
        entryFileNames: 'assets/[name]-[hash].js'
      }
    }
  }
});
```

### 代码质量约束

**TypeScript使用规范**：
```typescript
// ✅ 推荐：精确的类型定义
interface ApiResponse<T> {
  data: T;
  status: number;
  message: string;
}

// ✅ 推荐：类型安全的扩展
type ExtendedType = BaseType & {
  additionalProp?: string;
};

// ❌ 禁止：使用any绕过类型检查
const data: any = response;

// ❌ 禁止：粗暴的类型断言
const options = config as any;
```

**错误处理规范**：
```typescript
// ✅ 推荐：完整的错误处理
async function fetchData() {
  try {
    const response = await api.getData();
    return response.data;
  } catch (error) {
    console.error('Failed to fetch data:', error);
    // 提供降级方案
    return getDefaultData();
  }
}

// ❌ 避免：忽略错误处理
async function fetchData() {
  const response = await api.getData();
  return response.data;
}
```

## 🚀 性能优化约束

### 加载性能

**关键资源优化**：
- **关键CSS内联**：首屏CSS内联到HTML中
- **资源预加载**：使用 `<link rel="preload">` 预加载关键资源
- **DNS预解析**：使用 `<link rel="dns-prefetch">` 预解析域名

**代码分割策略**：
```javascript
// ✅ 推荐：按路由分割
const routes = [
  {
    path: '/',
    component: () => import('./pages/Home.vue')
  },
  {
    path: '/[功能路径]',
    component: () => import('./pages/[功能页面].vue')
  }
];

// ✅ 推荐：按功能分割
const [功能组件] = lazy(() => import('./components/[功能组件]'));
```

### 运行时性能

**框架优化**：
```javascript
// ✅ 推荐：使用memo避免不必要的重渲染
const MemoizedComponent = memo(({ data }) => {
  return <div>{data.title}</div>;
});

// ✅ 推荐：合理使用useCallback和useMemo
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

## 📱 PWA和现代Web特性

### Progressive Web App

**PWA基础要求**：
- **Manifest文件**：提供完整的Web App Manifest
- **Service Worker**：实现基础的缓存策略
- **HTTPS部署**：确保安全连接
- **响应式设计**：适配各种设备尺寸

**Service Worker注意事项**：
```javascript
// ✅ 推荐：开发环境跳过Service Worker
if (process.env.NODE_ENV === 'development') {
  // 开发环境不注册Service Worker
  console.log('Development mode: Service Worker disabled');
} else {
  // 生产环境注册Service Worker
  registerSW();
}
```

### 现代Web API使用

**API兼容性检查**：
```javascript
// ✅ 推荐：特性检测和降级
if ('IntersectionObserver' in window) {
  // 使用现代API
  const observer = new IntersectionObserver(callback);
} else {
  // 降级到传统方案
  window.addEventListener('scroll', scrollHandler);
}

// ✅ 推荐：Web Storage安全使用
function setStorageItem(key, value) {
  try {
    localStorage.setItem(key, JSON.stringify(value));
  } catch (error) {
    console.warn('localStorage not available:', error);
    // 使用内存存储作为降级
    memoryStorage[key] = value;
  }
}
```

## 🔍 SEO和可访问性约束

### SEO优化要求

**HTML语义化**：
```html
<!-- ✅ 推荐：语义化HTML结构 -->
<article>
  <header>
    <h1>文章标题</h1>
    <time datetime="2025-08-27">2025年8月27日</time>
  </header>
  <main>
    <p>文章内容...</p>
  </main>
</article>

<!-- ❌ 避免：过度使用div -->
<div class="article">
  <div class="title">文章标题</div>
  <div class="content">文章内容...</div>
</div>
```

**Meta标签完整性**：
```html
<!-- 基础SEO -->
<title>[页面标题] - [网站名称]</title>
<meta name="description" content="[页面描述]">
<meta name="keywords" content="[关键词1],[关键词2]">

<!-- Open Graph -->
<meta property="og:title" content="[页面标题]">
<meta property="og:description" content="[页面描述]">
<meta property="og:image" content="[部署域名]/images/og-image.jpg">
<meta property="og:url" content="[部署域名]/[页面路径]">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="[页面标题]">
<meta name="twitter:description" content="[页面描述]">
```

### 可访问性要求

**ARIA标签使用**：
```html
<!-- ✅ 推荐：提供ARIA标签 -->
<button aria-label="关闭对话框" onclick="closeDialog()">
  <span aria-hidden="true">&times;</span>
</button>

<nav aria-label="主导航">
  <ul role="menubar">
    <li role="menuitem"><a href="/">首页</a></li>
    <li role="menuitem"><a href="/about">关于</a></li>
  </ul>
</nav>
```

**键盘导航支持**：
```css
/* ✅ 推荐：明确的焦点样式 */
.button:focus {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}

/* ❌ 避免：移除焦点样式 */
.button:focus {
  outline: none;
}
```

## 🛠️ 调试和测试约束

### 开发调试

**Console使用规范**：
```javascript
// ✅ 推荐：开发环境调试信息
if (process.env.NODE_ENV === 'development') {
  console.log('Debug info:', data);
}

// ✅ 推荐：生产环境移除console
// 通过构建工具自动移除console.log

// ❌ 避免：生产环境保留调试信息
console.log('User data:', userData); // 可能泄露敏感信息
```

### 错误监控

**错误边界和处理**：
```javascript
// ✅ 推荐：全局错误处理
window.addEventListener('error', (event) => {
  console.error('Global error:', event.error);
  // 发送错误报告到监控服务
  reportError(event.error);
});

// ✅ 推荐：Promise错误处理
window.addEventListener('unhandledrejection', (event) => {
  console.error('Unhandled promise rejection:', event.reason);
  reportError(event.reason);
});
```

## ⚠️ 常见陷阱和避免事项

### Service Worker缓存问题

**开发环境预防**：
- 开发时优先使用无痕模式
- 定期清理Service Worker缓存
- 开发者工具中勾选"Bypass for network"

### 路径和部署问题

**常见路径问题**：
```javascript
// ❌ 错误：硬编码绝对路径
const imagePath = '/static/images/logo.png';

// ✅ 正确：使用相对路径或配置
const imagePath = process.env.PUBLIC_URL + '/images/logo.png';

// ✅ 正确：构建工具处理路径
import logoUrl from '/images/logo.png';
```

### 性能陷阱

**避免的性能问题**：
```javascript
// ❌ 避免：在render中创建对象
function Component() {
  return <Child style={{margin: 10}} />; // 每次render都创建新对象
}

// ✅ 推荐：提取到外部或使用useMemo
const childStyle = {margin: 10};
function Component() {
  return <Child style={childStyle} />;
}
```

## 📋 Web项目检查清单

### 开发阶段检查
- [ ] 选择的技术栈AI足够熟悉
- [ ] 构建配置符合静态站点要求
- [ ] 主题色和样式系统正确实现
- [ ] 响应式设计适配各种设备
- [ ] 代码质量符合TypeScript规范

### 部署前检查
- [ ] 构建产物结构符合要求（index.html + assets/）
- [ ] 所有资源路径正确配置
- [ ] SEO标签完整且正确
- [ ] 性能优化措施已实施
- [ ] 错误处理和降级方案完备

### 上线后验证
- [ ] 各种设备和浏览器测试通过
- [ ] 网站性能指标达标
- [ ] SEO检查工具验证通过
- [ ] 可访问性测试通过
- [ ] 错误监控正常工作

## 📊 项目特定约束

> **定制说明**：根据 [项目名称] 的特殊需求添加项目特定约束

### [技术栈] 特定约束
<!-- 可选章节开始 -->
- **框架版本**：[具体版本要求]
- **插件限制**：[允许或禁止的插件]
- **构建要求**：[特殊的构建配置]
- **部署约束**：[特殊的部署要求]
<!-- 可选章节结束 -->

### 业务逻辑约束
<!-- 可选章节开始 -->
- **数据处理**：[数据处理的特殊要求]
- **用户交互**：[用户交互的特殊约束]
- **安全要求**：[安全相关的特殊要求]
- **性能指标**：[具体的性能要求]
<!-- 可选章节结束 -->

---

**文档版本**：v1.0  
**创建日期**：[创建日期]  
**适用范围**：[项目名称] Web项目开发  
**更新说明**：基于Web项目经验整理的AI工作约束

**使用说明**：
1. 本文档与通用AI约束文档配合使用
2. Web项目开发时优先参考本文档的特定约束
3. 遇到冲突时，项目特定要求优先级更高
4. 定期根据新的Web技术发展更新约束内容

**定制提醒**：
- 替换所有占位符为实际项目信息
- 根据项目技术栈调整示例代码
- 删除不适用的可选章节
- 更新文档版本信息