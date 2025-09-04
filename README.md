# 文档模板使用指南

## 概述

这是一个可复用的文档模板库，包含了AI协作开发项目中常用的文档模板。这些模板基于实际项目经验整理而成，旨在帮助开发者快速建立项目文档体系，提高开发效率。

## 🚀 快速开始

### 1. 选择适合的模板组合

根据项目类型和需求，选择相应的文档模板：

#### AI协作项目（推荐）
```
✅ ai-guidelines/ai-working-constraints.md     # AI工作约束（必需）
✅ project-constraints.md                      # 项目约束规范
✅ project-troubleshooting.md                  # 问题排查指南
```

#### Web开发项目
```
✅ ai-guidelines/ai-working-constraints-web.md # Web项目AI约束
✅ project-deployment.md                       # 部署指南
✅ project-structure.md                        # 项目结构文档
✅ project-constraints.md                      # 项目约束规范
```

#### 完整项目（全套模板）
```
✅ 所有模板文档                                # 适用于复杂项目
```

### 2. 复制和定制流程

1. **复制模板文件**到你的项目文档目录
2. **替换占位符**：使用编辑器的查找替换功能批量替换
3. **删除不适用章节**：根据项目需求删除标记为"可选"的章节
4. **验证完整性**：使用检查清单确认定制完成

### 3. 占位符替换指南

#### 必需替换的占位符
| 占位符 | 说明 | 示例 |
|--------|------|------|
| `[项目名称]` | 项目的完整中文名称 | "在线学习平台" |
| `[项目英文名]` | 项目的英文标识符 | "online-learning-platform" |
| `[技术栈]` | 主要技术栈 | "React + Node.js + MongoDB" |
| `[部署域名]` | 生产环境域名 | "https://your-domain.com" |
| `[开发端口]` | 开发服务器端口 | "3000" |

#### 可选替换的占位符
| 占位符 | 说明 | 示例 |
|--------|------|------|
| `[团队名称]` | 开发团队名称 | "前端开发团队" |
| `[维护人员]` | 主要维护人员 | "张三 (zhang@your-domain.com)" |
| `[项目描述]` | 项目简短描述 | "基于AI的在线学习平台" |

## 📁 模板文档说明

### AI协作指南模板
- **[ai-guidelines/README.md](./ai-guidelines/README.md)** - AI指南使用说明
- **[ai-guidelines/ai-working-constraints.md](./ai-guidelines/ai-working-constraints.md)** - 通用AI工作约束模板
- **[ai-guidelines/ai-working-constraints-web.md](./ai-guidelines/ai-working-constraints-web.md)** - Web项目AI约束模板

### 项目管理模板
- **[project-background.md](./project-background.md)** - 项目背景和愿景模板
- **[project-constraints.md](./project-constraints.md)** - 项目约束和开发规范模板
- **[project-deployment.md](./project-deployment.md)** - 部署指南模板
- **[project-structure.md](./project-structure.md)** - 项目结构文档模板
- **[project-troubleshooting.md](./project-troubleshooting.md)** - 问题排查指南模板
- **[project-version.md](./project-version.md)** - 版本管理文档模板
- **[project-history-and-status.md](./project-history-and-status.md)** - 项目历史跟踪模板

### 使用指南
- **[template-guide.md](./template-guide.md)** - 详细的模板定制指南（AI和人类协作）

## 📋 AI约束记录快速指南

> **给AI助手的快速参考**：当用户提出新约束时，根据约束内容快速定位应该记录在哪个文档中。

### 🤖 约束分类和文档映射

#### AI行为约束 → `ai-guidelines/`
- **通用AI约束** → `ai-guidelines/ai-working-constraints.md`
  - 工作流程、需求确认、代码开发、文档操作、环境管理等
  - 适用于所有项目类型的AI行为规范
  
- **Web项目AI约束** → `ai-guidelines/ai-working-constraints-web.md`
  - 开发服务器管理、前端构建、部署配置、响应式设计等
  - 专门针对Web开发项目的AI约束

#### 项目技术约束 → 项目管理模板
- **开发规范约束** → `project-constraints.md`
  - 技术栈选择、代码规范、环境配置、安全要求等
  - 项目团队必须遵守的技术标准

- **部署相关约束** → `project-deployment.md`
  - 部署流程、服务器配置、环境变量、域名设置等
  - 项目部署和运维相关的约束

- **问题处理约束** → `project-troubleshooting.md`
  - 故障排查流程、问题记录格式、解决方案标准等
  - 问题处理和维护相关的约束

#### 项目管理约束 → 管理模板
- **版本管理约束** → `project-version.md`
  - 版本号规则、发布流程、回滚策略等
  - 版本控制和发布管理约束

- **项目历史约束** → `project-history-and-status.md`
  - 历史记录格式、状态跟踪、经验总结等
  - 项目历史和状态管理约束

### 🔍 快速判断流程

```
用户约束 → 判断约束类型 → 选择对应文档

1. 是否影响AI的工作方式？
   ├─ 是 → 是否Web开发特定？
   │   ├─ 是 → ai-working-constraints-web.md
   │   └─ 否 → ai-working-constraints.md
   └─ 否 → 继续判断

2. 是否是技术实现约束？
   ├─ 开发规范 → project-constraints.md
   ├─ 部署相关 → project-deployment.md
   ├─ 问题处理 → project-troubleshooting.md
   └─ 其他 → 继续判断

3. 是否是项目管理约束？
   ├─ 版本管理 → project-version.md
   ├─ 历史跟踪 → project-history-and-status.md
   ├─ 项目背景 → project-background.md
   └─ 项目结构 → project-structure.md
```

### 📝 常见约束类型示例

| 约束内容示例 | 约束类型 | 推荐文档 | 理由 |
|-------------|----------|----------|------|
| "启动服务器前检查端口" | AI行为(Web) | ai-working-constraints-web.md | Web开发特定的AI操作约束 |
| "代码提交前必须通过测试" | 项目技术 | project-constraints.md | 开发流程和质量标准 |
| "部署失败时自动回滚" | 部署相关 | project-deployment.md | 部署流程和策略 |
| "问题必须在24小时内响应" | 问题处理 | project-troubleshooting.md | 问题处理流程约束 |
| "版本号必须遵循语义化" | 版本管理 | project-version.md | 版本管理规范 |
| "重大决策必须记录原因" | 项目历史 | project-history-and-status.md | 历史跟踪要求 |

### ⚡ AI使用建议

1. **优先查看此快速指南** - 避免每次都分析所有文档
2. **按流程快速判断** - 使用判断流程树快速定位
3. **参考示例对照** - 通过示例表格快速匹配
4. **确认后再分析** - 确定目标文档后再详细分析章节位置
5. **遇到边界情况** - 提供2-3个选项让用户选择

## 🎯 使用场景

### 新项目启动
1. 复制AI协作基础模板
2. 根据技术栈选择对应的专业模板
3. 定制项目特定信息
4. 建立团队协作规范

### 现有项目规范化
1. 评估现有文档缺失
2. 选择需要补充的模板
3. 整合现有信息到模板中
4. 建立文档维护流程

### 团队标准化
1. 基于模板建立团队标准
2. 定制团队特定的约束和流程
3. 培训团队成员使用规范
4. 持续优化和更新标准

## ⚠️ 定制检查清单

使用模板前，请确认以下项目已完成：

### 占位符替换检查
- [ ] 搜索 `[项目名称]` 确认已全部替换
- [ ] 搜索 `[技术栈]` 确认技术信息准确
- [ ] 搜索 `[部署域名]` 确认域名配置正确
- [ ] 搜索 `[开发端口]` 确认端口无冲突
- [ ] 搜索 `[` 字符确认无遗漏的占位符

### 内容定制检查
- [ ] 删除了不适用的可选章节
- [ ] 更新了示例代码为实际技术栈
- [ ] 调整了约束条件符合项目需求
- [ ] 验证了文档间的交叉引用链接

### 完整性检查
- [ ] AI工作约束文档已包含并定制
- [ ] 项目约束文档符合实际需求
- [ ] 问题排查指南包含项目特定问题
- [ ] 文档版本信息已更新

## 🔧 高级定制

### 添加项目特定章节
```markdown
## [项目特定功能] 约束

> **定制说明**：根据项目特殊需求添加的约束章节

### 特殊要求
- 具体的项目约束...
```

### 自定义占位符
如果项目有特殊需求，可以定义额外的占位符：
```
[数据库类型] → MySQL/PostgreSQL/MongoDB
[缓存系统] → Redis/Memcached
[消息队列] → RabbitMQ/Kafka
```

### 模板组合策略
```markdown
# 小型项目组合
- ai-working-constraints.md
- project-constraints.md
- project-troubleshooting.md

# 中型项目组合
+ project-deployment.md
+ project-structure.md

# 大型项目组合
+ project-background.md
+ project-version.md
+ project-history-and-status.md
```

## 📚 相关资源

### 模板维护
- **更新频率**：建议每季度检查模板是否需要更新
- **版本管理**：使用语义化版本号管理模板版本
- **反馈机制**：收集使用反馈，持续改进模板质量

### 扩展阅读
- **AI协作最佳实践** - [根据项目需要添加相关链接]
- **项目文档标准** - [根据项目需要添加相关链接]
- **团队协作规范** - [根据项目需要添加相关链接]

## 🤝 贡献指南

### 如何贡献
1. **发现问题**：使用过程中发现的问题或改进建议
2. **提交反馈**：通过Issue或Pull Request提交
3. **分享经验**：分享成功的项目实践和定制经验
4. **完善模板**：基于实际使用经验完善模板内容

### 贡献原则
- **基于实践**：贡献内容应基于实际项目经验
- **保持通用**：避免过于特定的项目信息
- **质量优先**：确保贡献内容的质量和准确性
- **向后兼容**：考虑对现有使用者的影响

---

**模板库版本**：v1.0  
**创建日期**：2025-08-27  
**适用范围**：AI协作开发项目  
**维护状态**：活跃维护

**使用统计**：
- 模板总数：11个
- AI协作模板：3个
- 项目管理模板：8个
- 支持项目类型：Web开发、AI协作、通用项目