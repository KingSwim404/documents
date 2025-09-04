# [项目名称] 问题排查指南

<!-- 
使用说明：
1. 将 [项目名称] 替换为你的实际项目名称
2. 根据项目技术栈调整具体的技术细节
3. 添加项目特有的问题和解决方案
4. 定期更新和维护问题记录
5. 可选章节用 HTML 注释标记，根据需要保留或删除
-->

## 文档目的
记录项目开发过程中常见问题和解决方案，便于快速查找和解决类似问题。适用于 [技术栈描述，如：Vue/React等SPA项目]。

## 🌐 浏览器相关问题

### 问题1：Service Worker缓存导致页面空白和刷新失败
**现象：** 
- 正常浏览器打开开发地址显示空白页面
- 无痕浏览器打开同样地址显示正常
- 控制台显示：`Service Worker: Serving from cache`
- 错误信息：`Failed to load module script: Expected a JavaScript-or-Wasm module script but the server responded with a MIME type of ""`

**原因：** 
- Service Worker缓存了旧版本或损坏的文件
- 缓存文件的MIME类型不正确
- Service Worker优先级高于新的开发服务器

**解决方案（按顺序尝试）：**

1. **彻底清除Service Worker**（最有效）
   - 开发者工具 (F12) → Application → Service Workers
   - 找到对应域名的Service Worker
   - 点击 "Unregister" 注销
   - 刷新页面

2. **清除所有本地数据**
   - 开发者工具 → Application → Storage
   - 点击 "Clear storage" 清除所有数据
   - 包括：Cache Storage, Local Storage, Session Storage等

3. **强制刷新**
   - 右键点击刷新按钮
   - 选择 "清空缓存并硬性重新加载"

4. **终极方案：重置浏览器状态**
   - 关闭所有相关标签页
   - 清除浏览器数据
   - 重新打开页面

**预防措施：**

1. **开发时使用无痕模式**（最有效）
   - 无痕模式不会使用Service Worker
   - 不会有任何缓存干扰
   - 每次都是全新环境

2. **使用不同端口开发不同项目**
   - 避免端口冲突和缓存混淆
   - 每个项目独立的缓存空间

3. **定期清理开发环境**
   - 项目切换时清理Service Worker
   - 定期清理浏览器开发数据

4. **禁用Service Worker（开发时）**
   - 开发者工具 → Application → Service Workers
   - 勾选 "Bypass for network" 选项
   - 开发时跳过Service Worker缓存

### 问题2：SPA路由刷新后页面空白
**现象：** 
- 首次访问页面正常显示
- 浏览器刷新后页面变空白
- 清除缓存后能临时恢复，但再次刷新又空白

**原因：** 
- SPA路由配置问题
- [路由库名称，如：Vue Router/React Router] 的history模式配置不正确
- 缺少catch-all路由处理未匹配路径

**解决方案：**
1. **修复路由配置**
   ```typescript
   // [根据项目技术栈调整代码示例]
   // Vue Router 示例
   const router = createRouter({
     history: createWebHistory('/'),  // 明确指定base路径
     routes
   })
   
   // React Router 示例
   <BrowserRouter basename="/">
     <Routes>
       {/* 路由配置 */}
     </Routes>
   </BrowserRouter>
   ```

2. **添加catch-all路由**
   ```typescript
   // [根据项目路由库调整]
   // Vue Router 示例
   {
     path: '/:pathMatch(.*)*',
     redirect: '/'  // 未匹配路由重定向到首页
   }
   
   // React Router 示例
   <Route path="*" element={<Navigate to="/" replace />} />
   ```

3. **检查组件导入路径**
   ```typescript
   component: () => import('../pages/[页面名称].vue')  // ✅ 使用相对路径
   ```

### 问题3：浏览器缓存导致更新不生效
**现象：**
- 代码已更新但浏览器显示旧版本
- 强制刷新后才能看到更新

**解决方案：**
1. **开发环境禁用缓存**
   - 开发者工具 → Network → 勾选 "Disable cache"

2. **构建时添加版本号**
   ```javascript
   // [根据构建工具调整配置]
   // Vite配置示例
   build: {
     rollupOptions: {
       output: {
         entryFileNames: 'assets/[name]-[hash].js',
         chunkFileNames: 'assets/[name]-[hash].js',
         assetFileNames: 'assets/[name]-[hash][extname]'
       }
     }
   }
   ```

## 🔧 开发环境问题

### 问题4：TypeScript路径别名不识别
**现象：** 
- IDE显示 `Cannot find module '@/components/xxx'` 错误
- 编译时找不到模块

**原因：** 
- TypeScript配置与构建工具配置不匹配
- 路径别名配置不正确

**解决方案：**
1. **使用相对路径**（临时方案）
   ```typescript
   import('../components/[组件名称].vue')  // 而不是 import('@/components/[组件名称].vue')
   ```

2. **修复TypeScript配置**（长期方案）
   ```json
   // tsconfig.json
   {
     "compilerOptions": {
       "paths": {
         "@/*": ["./src/*"]
       }
     }
   }
   ```

3. **确保构建工具配置匹配**
   ```javascript
   // [根据构建工具调整]
   // vite.config.ts 示例
   resolve: {
     alias: {
       '@': resolve(__dirname, 'src')
     }
   }
   ```

### 问题5：依赖安装失败
**现象：** 
- `[包管理器命令，如：npm install]` 执行失败
- 依赖版本冲突

**解决方案：**
1. **清理缓存**
   ```bash
   # [根据使用的包管理器调整命令]
   npm cache clean --force
   rm -rf node_modules package-lock.json
   npm install
   
   # 或使用 yarn
   yarn cache clean
   rm -rf node_modules yarn.lock
   yarn install
   ```

2. **检查Node.js版本**
   - 确保使用兼容的Node.js版本
   - 建议使用LTS版本
   - 检查项目的 `.nvmrc` 或 `engines` 字段

3. **使用替代包管理器**
   ```bash
   # 如果npm有问题，尝试yarn或pnpm
   yarn install
   # 或
   pnpm install
   ```

### 问题6：端口被占用
**现象：** 
- 启动开发服务器时提示端口被占用
- 服务器启动在错误的端口

**解决方案：**
1. **杀死占用端口的进程**
   ```bash
   # 查找占用端口的进程
   lsof -i :[端口号]  # 替换为实际端口号，如 :3000
   
   # 杀死进程
   kill -9 <PID>
   
   # 或者杀死所有node进程
   pkill -f node
   ```

2. **使用其他端口**
   - 修改配置文件中的端口设置
   - 或使用命令行参数指定端口

## 🎨 样式相关问题

### 问题7：CSS变量不生效
**现象：** 
- 定义的CSS变量无法使用
- 样式显示异常

**解决方案：**
1. **检查CSS导入顺序**
   ```typescript
   // [入口文件，如：main.ts] 中确保样式文件被正确导入
   import './styles/index.css'
   ```

2. **检查CSS变量定义**
   ```css
   :root {
     --primary-color: [主色调];  /* 确保变量定义正确 */
     --secondary-color: [次要色调];
   }
   
   .component {
     color: var(--primary-color);  /* 使用变量 */
   }
   ```

### 问题8：样式不生效或被覆盖
**现象：**
- CSS样式写了但不生效
- 样式被其他样式覆盖

**解决方案：**
1. **检查CSS选择器优先级**
   ```css
   /* 提高优先级 */
   .parent .child.specific-class {
     /* 样式 */
   }
   ```

2. **使用CSS Modules或Scoped CSS**
   ```vue
   <!-- [根据框架调整] -->
   <!-- Vue示例 -->
   <style scoped>
   .component {
     /* 样式只作用于当前组件 */
   }
   </style>
   ```

3. **检查样式加载顺序**
   - 确保自定义样式在第三方库样式之后加载

## 🚀 构建和部署问题

### 问题9：构建失败
**现象：**
- `[构建命令，如：npm run build]` 执行失败
- 出现编译错误

**解决方案：**
1. **检查TypeScript类型错误**
   ```bash
   [类型检查命令，如：npm run type-check]  # 或 tsc --noEmit
   ```

2. **检查ESLint错误**
   ```bash
   [代码检查命令，如：npm run lint]
   ```

3. **清理构建缓存**
   ```bash
   rm -rf [构建输出目录，如：dist/]
   rm -rf node_modules/.cache/
   ```

### 问题10：生产环境路径问题
**现象：**
- 本地开发正常，部署后资源加载失败
- 404错误或路径不正确

**解决方案：**
1. **检查base路径配置**
   ```javascript
   // [根据构建工具调整]
   // vite.config.ts 示例
   export default defineConfig({
     base: '/[部署路径]/',  // 根据部署路径调整
   })
   ```

2. **使用相对路径**
   ```javascript
   // 避免硬编码绝对路径
   const imagePath = './assets/[图片名称].png'  // ✅
   const imagePath = '/assets/[图片名称].png'   // ❌ 可能在子目录部署时失效
   ```

<!-- 可选：移动端相关问题，如果项目不涉及移动端可删除此章节 -->
## 📱 移动端问题

### 问题11：移动端样式异常
**现象：**
- 桌面端正常，移动端显示异常
- 触摸事件不响应

**解决方案：**
1. **添加viewport meta标签**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```

2. **使用响应式设计**
   ```css
   @media (max-width: 768px) {
     .component {
       /* 移动端样式 */
     }
   }
   ```

3. **处理触摸事件**
   ```javascript
   // 添加触摸事件支持
   element.addEventListener('touchstart', handleTouch)
   ```
<!-- 移动端问题章节结束 -->

## 🔍 调试技巧

### 通用调试方法
1. **使用浏览器开发者工具**
   - Console：查看错误信息和日志
   - Network：检查网络请求
   - Sources：断点调试
   - Application：检查存储和缓存

2. **添加调试日志**
   ```javascript
   console.log('[调试信息]:', data)
   console.error('[错误信息]:', error)
   ```

3. **使用框架开发者工具**
   - 安装对应的浏览器扩展（如：[Vue/React] DevTools）
   - 检查组件状态和props

### 性能调试
1. **使用Performance面板**
   - 分析页面加载性能
   - 找出性能瓶颈

2. **使用Lighthouse**
   - 自动化性能分析
   - 获得优化建议

## 📝 问题记录模板

遇到新问题时，请按以下格式记录：

```markdown
### 问题X：[问题简述]
**现象：** 
- [具体现象描述]

**原因：** 
- [问题原因分析]

**解决方案：**
1. **[解决方案1]**
   ```code
   // 代码示例
   ```

2. **[解决方案2]**
   - [步骤说明]

**状态：** [已解决/待验证/已知问题]
```

## 🛠️ 预防措施

### 开发最佳实践
1. **使用版本控制**
   - 定期提交代码
   - 使用有意义的提交信息

2. **代码审查**
   - 团队成员互相审查代码
   - 使用自动化检查工具

3. **测试驱动开发**
   - 编写单元测试
   - 集成测试覆盖关键功能

4. **文档维护**
   - 及时更新项目文档
   - 记录重要的技术决策

### 环境管理
1. **使用容器化**（可选）
   - 使用Docker统一开发环境
   - 避免"在我机器上能跑"问题

2. **环境变量管理**
   - 使用.env文件管理配置
   - 不同环境使用不同配置

3. **依赖版本锁定**
   - 使用package-lock.json或yarn.lock
   - 定期更新依赖版本

## 📚 参考资源

### 官方文档
- **[框架名称]官方文档** - [根据实际框架添加官方文档链接]
- **[构建工具名称]官方文档** - [根据实际构建工具添加官方文档链接]
- [TypeScript官方文档](https://www.typescriptlang.org/)

### 调试工具
- **[框架] DevTools** - [根据实际框架添加开发者工具链接]
- [Chrome DevTools](https://developer.chrome.com/docs/devtools/)

### 社区资源
- [Stack Overflow](https://stackoverflow.com/)
- [GitHub Issues](https://github.com/)
- [MDN Web Docs](https://developer.mozilla.org/)

<!-- 可选：项目特定资源 -->
### 项目特定资源
- [项目内部文档链接]
- [团队知识库链接]
- [相关项目参考链接]
<!-- 项目特定资源结束 -->

---

**文档版本：** v1.0  
**创建日期：** [创建日期]  
**适用范围：** [项目名称] - [技术栈描述]  
**维护人员：** [维护人员姓名/团队]

**使用说明：**
1. 遇到问题时先在此文档中搜索类似问题
2. 解决问题后及时更新此文档，记录解决方案
3. 定期维护，整理和优化解决方案，移除过时信息
4. 根据项目特点添加项目特定的问题和解决方案
5. 与团队成员分享新发现的问题和解决方案