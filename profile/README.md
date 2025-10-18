# Call Center Organization

> **外呼业务管理系统** - 基于微服务架构的完整解决方案

---

## 📋 项目简介

Call Center Organization 是一个现代化的外呼业务管理系统，采用**微服务架构**，每个业务模块独立部署和维护。

### 🎯 核心特点

- 🔧 **微服务架构** - 每个服务独立仓库，完全解耦
- 🤖 **AI 驱动开发** - 非技术背景团队使用 Cursor/Claude 进行全栈开发
- 📊 **数据驱动** - 完整的数据采集、处理、分析闭环
- 🚀 **快速迭代** - 各服务独立开发，互不影响

### 📚 文档导航

- **本文档** (Organization README)：整体架构 + AI 开发流程
- **[call-center-docs](https://github.com/call-center-org/call-center-docs)**：详细的技术文档、API规范、部署指南

---

## 🎛️ 通俗易懂沟通模式（默认开启）

### 💡 什么是"通俗易懂模式"？

本项目的用户是**非技术背景**的业务人员，因此 AI 默认使用**通俗易懂沟通模式**。

在这个模式下，AI 会：
- 用生活化的类比解释技术概念（盖房子、记账本、Excel 等）
- 避免技术术语，或先解释再使用
- 用表情符号和视觉元素让内容更易读（✅❌🎯💡📊）
- 给出明确的选项，而不是问开放性问题
- 详细解释"为什么"，而不只是"做什么"

### 🔄 如何切换模式？

项目提供 **2 种沟通模式**，可随时切换：

#### 🟢 通俗易懂模式（默认）

**每次新对话开始时，AI 会提示**：
```
🟢 通俗易懂模式：已开启

我会用通俗的语言跟您交流。
如果您想切换到专业模式，请说：「关闭通俗易懂模式」
```

**特点**：
- 用生活化类比（盖房子、记账本等）
- 详细解释概念
- 表情符号 + 视觉元素
- 给明确选项（A/B/C）

---

#### 🔵 专业模式（可选）

**切换命令**，您可以随时说：
```
关闭通俗易懂模式
或
切换到专业模式
或
使用技术语言
```

**AI 会确认**：
```
🔵 专业模式：已开启

我将使用标准技术术语，简洁直接地回答。
如果想切换回通俗易懂模式，请说：「开启通俗易懂模式」
```

**特点**：
- 使用标准技术术语
- 简洁直接的回答
- 假设用户理解基础概念
- 快速执行，减少解释

---

#### 🟢 切换回通俗易懂模式

**切换命令**，您可以随时说：
```
开启通俗易懂模式
或
切换到通俗模式
或
用简单的语言
```

**AI 会确认**：
```
🟢 通俗易懂模式：已开启

我将用通俗易懂的方式跟您交流。
```

---

### 📋 两种模式的对比示例

#### 示例：解释"数据库迁移"

**🟢 通俗易懂模式**：
```
想象您有一个 Excel 表格 📊：
- 最开始有 5 列（ID、名称、来源、总数、成本）
- 现在需要加 15 列（N层、O1层...O15层）

"数据库迁移"就是：
1. 记录这个变化（加了哪些列）
2. 程序自动给现有数据的新列填默认值（比如填 0）
3. 以后如果出问题，可以回退（就像 Ctrl+Z）

这样您就不用手动去数据库里加列，程序会自动帮您做。

明白了吗？😊
```

**🔵 专业模式**：
```
数据库迁移使用 Alembic 管理 SQLAlchemy 模型的版本控制。

执行步骤：
1. flask db migrate -m "添加层级字段"
2. flask db upgrade

需要我执行吗？
```

---

### 🎯 模式切换规则

| 场景 | 默认模式 | 说明 |
|------|---------|------|
| 新对话窗口 | 🟢 通俗易懂 | 每次都从通俗模式开始 |
| 用户主动要求 | 按用户指定 | 立即切换 |
| 同一对话内 | 保持当前模式 | 直到用户要求切换 |

---

### ⚠️ 重要提醒

**无论在哪种模式下，AI 都必须**：
1. ✅ 先读取 Organization README
2. ✅ 主动询问要开发哪个子系统
3. ✅ 等待用户确认后再执行
4. ✅ 严格遵循 PRD 和里程碑规划

**模式切换只影响沟通风格，不影响开发流程。**

---

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────┐
│                     统一前端看板（规划中）                     │
│           聚合展示所有子系统的关键数据和指标                    │
└─────────────────────────────────────────────────────────────┘
                              ↓
        ┌─────────────────────┼─────────────────────┐
        ↓                     ↓                     ↓
┌───────────────┐    ┌───────────────┐    ┌──────────────┐
│  外呼数据系统  │    │  线索管理系统  │    │  桌面小部件   │
│ business-data │    │lead-management│    │  widget-mac  │
└───────────────┘    └───────────────┘    └──────────────┘
        ↓                     ↓                     ↓
    从第三方平台           管理线索数据            快捷查看数据
    获取外呼数据           创建外呼任务            (macOS 插件)
    进行数据分析           成本预算分析
```

### 📡 服务间通信

- 通过 **RESTful API** 进行数据交互
- API 规范文档统一维护在 [`call-center-docs`](https://github.com/call-center-org/call-center-docs)
- 每个服务可独立运行，也可组合使用

---

## 📦 子系统列表

### 1. 🎯 [线索管理系统](https://github.com/call-center-org/call-center-lead-management)

**状态**: 🔄 开发中 (M1 阶段)

**功能**:
- 📦 线索数据包管理（采买、登记、追踪）
- 📞 外呼任务创建（与第三方平台对接）
- 📊 任务数据回收与标签统计
- 💰 成本分析与采买策略（日/周/月报）
- 🧮 线索需求预测与预算规划

**技术栈**: React + Vite + Flask + SQLAlchemy + PostgreSQL

**端口**: 前端 3002 / 后端 5002

**文档**: 
- [README](https://github.com/call-center-org/call-center-lead-management/blob/main/README.md)
- [PRD](https://github.com/call-center-org/call-center-lead-management/blob/main/docs/线索管理系统_PRD.md)
- [里程碑跟踪](https://github.com/call-center-org/call-center-lead-management/blob/main/docs/MILESTONE_TRACKING.md)

---

### 2. 📊 [外呼数据系统](https://github.com/call-center-org/call-center-business-data)

**状态**: ✅ 已上线

**功能**:
- 📡 从第三方外呼平台调取通话数据
- 🔄 数据二次处理与清洗
- 📈 多维度数据统计与分析
- 📊 数据可视化展示

**技术栈**: React + Vite + Tailwind CSS

**端口**: 3001

**部署**: [CloudBase](https://cloud1-6gt5ulxm10210d0f.ap-shanghai.app.tcloudbase.com/data/)

**文档**: [README](https://github.com/call-center-org/call-center-business-data/blob/main/README.md)

---

### 3. 🖥️ [桌面小部件 (macOS)](https://github.com/call-center-org/call-center-widget-mac)

**状态**: ✅ 生产可用 (v1.0.2)

**功能**:
- 🚀 快捷查看外呼数据
- 📊 实时数据刷新
- 🎨 美观的 macOS 原生界面
- 🔄 自动刷新（30秒可配置）
- ⚙️ 灵活配置管理

**技术栈**: Electron 27.0 + Axios + electron-store

**文档**: [README](https://github.com/call-center-org/call-center-widget-mac/blob/main/README.md)

---

### 4. 📚 [文档仓库](https://github.com/call-center-org/call-center-docs)

**状态**: ✅ 持续更新

**内容**:
- 📖 产品需求文档（PRD）
- 📡 API 接口规范
- 🏗️ 系统架构文档
- 🚀 部署指南与问题排查
- 💡 开发经验与踩坑总结
- 🤝 团队协作规范

**重要文档**:
- [API 规范](https://github.com/call-center-org/call-center-docs/tree/main/api)
- [架构文档](https://github.com/call-center-org/call-center-docs/tree/main/architecture)
- [部署指南](https://github.com/call-center-org/call-center-docs/tree/main/deployment)

---

## 🚀 快速开始

### 对于开发者

#### 1. **首次接触项目？**

👉 **先阅读本 README**，了解整体架构

#### 2. **要开发某个子系统？**

👉 **进入对应仓库**，阅读该子系统的 README

例如开发线索管理系统：
```bash
# 1. 克隆仓库
git clone https://github.com/call-center-org/call-center-lead-management.git

# 2. 阅读 README（必读）
cat README.md

# 3. 查看详细文档
cat docs/线索管理系统_PRD.md
cat docs/MILESTONE_TRACKING.md

# 4. 开始开发...
```

#### 3. **需要对接其他服务的 API？**

👉 **查看文档仓库** 的 API 规范
```bash
git clone https://github.com/call-center-org/call-center-docs.git
cd call-center-docs/api/
```

---

## 🤖 AI 协作指南

> **本项目由非技术背景团队使用 AI (Cursor/Claude) 进行全栈开发**

### 🎯 核心原则

1. **每个子系统独立开发**
   - 打开新对话窗口时，先进入对应的子系统目录
   - 阅读该子系统的 `README.md`（必读）
   - 按照子系统的文档规范进行开发

2. **遵循各子系统的规则**
   - 每个子系统有自己的 PRD、里程碑规划、开发规范
   - **不要**跨子系统乱套规则
   - **不要**根据记忆或猜测，一切以文档为准

3. **API 对接规范**
   - 服务间调用必须查阅 `call-center-docs/api/` 的规范
   - 不得擅自修改 API 接口定义

### 📖 AI 开发流程（必须严格遵守）

**🚨 当打开新的对话窗口时，必须按以下步骤进行：**

```
Step 1: 📖 读取 Organization README（本文档）
        了解整体架构和所有子系统
        ↓
Step 2: 🤔 主动询问用户
        "我看到这是一个微服务架构的项目，包含以下子系统：
         1. 线索管理系统 (call-center-lead-management)
         2. 外呼数据系统 (call-center-business-data)
         3. 桌面小部件 (call-center-widget-mac)
         4. 文档仓库 (call-center-docs)
         
         请问您现在要开发哪个子系统？"
        ↓
Step 3: ⏳ 等待用户明确回答
        ❌ 不要假设或猜测
        ❌ 不要根据上下文自行判断
        ✅ 必须等用户明确指定
        ↓
Step 4: 📂 进入对应子系统目录
        用户回答："线索管理系统"
        → cd call-center-lead-management/
        ↓
Step 5: 📖 读取子系统 README（🚨 必读）
        完整阅读该子系统的 README.md
        了解该子系统的：
        - 核心原则（唯一需求来源等）
        - 里程碑划分（M0-M4）
        - 开发流程
        - AI 协作规则
        ↓
Step 6: 📚 读取子系统详细文档
        - docs/xxx_PRD.md（产品需求）
        - docs/MILESTONE_TRACKING.md（进度跟踪）
        ↓
Step 7: 💬 向用户确认当前状态
        "我看到：
         - 当前阶段：M1 - Cursor 骨架
         - 进度：前端 0/15，后端 0/18
         请问要从哪个任务开始？"
        ↓
Step 8: 🚀 开始开发
        严格按照子系统的规则和当前里程碑进行
        ↓
Step 9: ✅ 完成后更新进度文档
        更新 docs/MILESTONE_TRACKING.md
        标记已完成的任务 [x]
```

### ⚠️ AI 禁止行为

**以下行为严格禁止：**

1. ❌ **不要假设用户要开发哪个子系统**
   - 即使用户之前的对话提到过某个系统
   - 即使文件路径显示在某个系统目录
   - 必须明确询问用户

2. ❌ **不要跳过 Organization README**
   - 即使用户直接说"开发线索管理系统"
   - 也要先读 Organization README 了解整体
   - 然后再进入子系统

3. ❌ **不要混淆不同子系统的规则**
   - 线索管理系统：使用 M0-M4 里程碑
   - 外呼数据系统：可能有自己的规划
   - 每个系统独立，不要串用

4. ❌ **不要根据记忆开发**
   - 所有决策必须基于文档
   - 不要说"我记得..."
   - 不要说"通常是..."

5. ❌ **不要擅自修改需求**
   - PRD 是唯一的需求来源
   - 不要根据"最佳实践"改需求
   - 发现问题要先询问用户

### ✅ 正确的对话示例

**场景：新窗口开始开发**

```
🤖 AI: 你好！我注意到这是一个 Call Center Organization 项目。
       让我先阅读 Organization README 了解整体架构...
       
       [AI 读取 ORGANIZATION_README.md]
       
       好的，我了解到这是一个微服务架构，包含以下子系统：
       
       1. 📦 线索管理系统 (call-center-lead-management)
          功能：线索采买、任务管理、成本分析
          状态：开发中 - M1 阶段
       
       2. 📊 外呼数据系统 (call-center-business-data)
          功能：从第三方平台获取和分析数据
          状态：已上线
       
       3. 🖥️ 桌面小部件 (call-center-widget-mac)
          功能：macOS 快捷查看工具
          状态：开发中
       
       4. 📚 文档仓库 (call-center-docs)
          功能：共享文档和 API 规范
       
       请问您现在要开发哪个子系统？

👤 用户: 线索管理系统

🤖 AI: 好的！让我进入线索管理系统目录并读取 README...
       
       [AI 读取 call-center-lead-management/README.md]
       
       我看到了以下关键信息：
       
       ⚠️ 核心原则：
       1. 唯一需求来源：docs/线索管理系统_PRD.md
       2. 唯一里程碑划分：M0-M4（不使用 Phase）
       3. 唯一进度跟踪：docs/MILESTONE_TRACKING.md
       
       📊 当前状态：
       - M0：Figma 低保真 ✅ 已完成
       - M1：Cursor 骨架 🔄 进行中（0%）
         - 前端任务：0/15
         - 后端任务：0/18
       
       现在让我查看详细的进度跟踪...
       
       [AI 读取 MILESTONE_TRACKING.md]
       
       明白了！M1 阶段需要完成：
       - 前端：项目搭建、4个页面骨架
       - 后端：Flask搭建、数据库模型、基础API
       
       请问要从哪个任务开始？前端还是后端？
```

### ❌ 错误的对话示例

**❌ 错误 1：直接假设**
```
AI: 好的，我们开始开发线索管理系统...
```
→ 错在没有先问用户要开发哪个系统

**❌ 错误 2：用错里程碑**
```
AI: 现在在 Phase 2 阶段，我们需要...
```
→ 错在没有读子系统 README，用了错误的里程碑划分

**❌ 错误 3：根据记忆**
```
AI: 根据我的理解，我们应该先做用户认证...
```
→ 错在没有查阅 PRD 和 MILESTONE_TRACKING

**❌ 错误 4：跳过询问**
```
用户: 帮我开发首页看板
AI: 好的，开始创建 Dashboard.jsx...
```
→ 错在没有先确认是哪个子系统的首页看板

---

## 📂 项目结构

```
call-center-org/                      # GitHub Organization
├── call-center-business-data/        # 外呼数据系统
│   ├── README.md                     # 📖 子系统入口文档
│   ├── src/                          # 源代码
│   └── ...
│
├── call-center-lead-management/      # 线索管理系统
│   ├── README.md                     # 📖 子系统入口文档（🚨 必读）
│   ├── docs/
│   │   ├── 线索管理系统_PRD.md       # 产品需求
│   │   └── MILESTONE_TRACKING.md     # 里程碑跟踪
│   ├── frontend/                     # React 前端
│   ├── backend/                      # Flask 后端
│   └── ...
│
├── call-center-widget-mac/           # 桌面小部件
│   ├── README.md                     # 📖 子系统入口文档
│   ├── src/                          # Electron 源码
│   └── ...
│
└── call-center-docs/                 # 📚 文档仓库（共享）
    ├── README.md                     # 文档索引
    ├── api/                          # API 规范
    │   ├── business-system.md
    │   ├── data-system.md
    │   └── ...
    ├── architecture/                 # 架构文档
    ├── deployment/                   # 部署指南
    └── contexts/                     # 上下文文档（AI 协作）
```

---

## 🔗 重要链接

### 📦 GitHub 仓库（各司其职）

| 仓库 | 定位 | 链接 |
|------|------|------|
| 🏠 **.github** | Organization 主页（你正在看的文档） | [call-center-org](https://github.com/call-center-org) |
| 📚 **call-center-docs** | 详细技术文档、API规范、部署指南 | [查看仓库](https://github.com/call-center-org/call-center-docs) |
| 🎯 **线索管理系统** | 微服务：线索采买、任务管理、成本分析 | [查看仓库](https://github.com/call-center-org/call-center-lead-management) |
| 📊 **外呼数据系统** | 微服务：外呼数据采集、二次处理 | [查看仓库](https://github.com/call-center-org/call-center-business-data) |
| 🖥️ **桌面小部件** | 微服务：macOS 桌面快捷查看工具 | [查看仓库](https://github.com/call-center-org/call-center-widget-mac) |

### 🚀 生产环境
- 📊 外呼数据系统: https://cloud1-6gt5ulxm10210d0f.ap-shanghai.app.tcloudbase.com/data/
- 🎯 线索管理系统: https://call-center-frontend.zeabur.app

---

## 🛠️ 技术栈

- **前端**: React + Vite + TailwindCSS
- **后端**: Flask + SQLAlchemy
- **数据库**: PostgreSQL / SQLite
- **部署**: Zeabur / CloudBase
- **认证**: JWT

📚 **详细的技术文档**: [call-center-docs](https://github.com/call-center-org/call-center-docs)

---

## 📅 开发状态

| 系统 | 状态 | 当前阶段 | 负责人 |
|------|------|----------|--------|
| 线索管理系统 | 🔄 开发中 | M1 - Cursor 骨架 | Tom (tom88115) |
| 外呼数据系统 | ✅ 已上线 | 生产运行 | Tom (tom88115) |
| 桌面小部件 | ✅ 生产可用 | v1.0.2 已发布 | Tom (tom88115) |
| 统一前端看板 | 📅 规划中 | 需求调研 | 待定 |

---

## 🤝 团队与协作

### 团队成员
- **Tom** (@tom88115) - 线索管理系统、外呼数据系统、桌面小部件
- **Partner** - ERP 系统（规划中）

### 协作方式
- 📝 所有共享文档在 `call-center-docs` 仓库
- 💬 Issue 跟踪在各子系统仓库
- 🔄 通过 Pull Request 进行代码审查
- 🤖 使用 AI (Cursor/Claude) 辅助开发

### 贡献指南
1. Fork 对应的子系统仓库
2. 创建功能分支 (`git checkout -b feature/xxx`)
3. 提交更改 (`git commit -m 'Add xxx'`)
4. 推送分支 (`git push origin feature/xxx`)
5. 创建 Pull Request

---

## 📝 开发规范

- **仓库命名**: `call-center-{service-name}`
- **提交规范**: 使用 emoji 前缀（📚 文档 / ✨ 新功能 / 🐛 修复）
- **文档要求**: 每个子系统必须有 README.md

📚 **详细的开发规范**: [call-center-docs/development/](https://github.com/call-center-org/call-center-docs/tree/main/development)

---

## 🎯 未来规划

- **短期**: 完成各子系统的核心功能（M0-M2）
- **中期**: 建立微服务整合看板（统一前端）
- **长期**: 完整的数据分析和智能决策系统

📚 **详细的产品路线图**: [call-center-docs/business/roadmap.md](https://github.com/call-center-org/call-center-docs/tree/main/business)

---

## ⚠️ 重要提示

### 对于 AI（Cursor/Claude）

1. **每次打开新对话窗口**：
   - 先阅读本 README 了解整体架构
   - 确认要开发的子系统
   - 进入子系统目录，阅读该系统的 README

2. **开发时**：
   - 严格遵循子系统的文档规范
   - 不要跨系统混淆规则
   - 有疑问查阅 `call-center-docs`

3. **完成后**：
   - 更新子系统的进度文档
   - 如有 API 变更，更新 `call-center-docs`

---

## 📞 联系方式

**团队**: 江苏职场呼叫中心  
**维护者**: Tom (@tom88115)  
**GitHub**: https://github.com/tom88115

---

## 📄 许可证

[待定 - 建议使用 MIT License]

---

**最后更新**: 2025-10-18  
**文档版本**: 1.1

