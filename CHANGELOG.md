# Changelog

本仓库整体的变更记录。各 skill 内部的细粒度变更记录在各自 `SKILL.md` 末尾的 CHANGELOG 块中。

## [Unreleased]

## [0.3.3] - 2026-05-20

### Changed

- 重写两个 skill 的 `context/glossary.md`，采用 3 节结构：
  1. **撰写基本术语**：skill 工作流必备词汇（FR / 子模块 / P0 / 数据类型 / 触发类型等），固定保留
  2. **业务术语示例**（SRM 领域）：作为示范骨架，实际起草时按用户领域临时增补
  3. **用户领域术语**（按需追加）：起草过程中遇到新术语时按指定格式追加，作为后续起草参考
- 砍掉旧版中冗余的"反复出现的疑问与统一答复""历史修订记录""高价值机制"等节段（这些归 memory）
- 与 business-background 的设计理念保持一致：SRM 仅作示例，使用过程中按用户描述补充

## [0.3.2] - 2026-05-20

### Changed

- 重写两个 skill 的 `context/business-background.md`：
  - 从原来的"方法论与协作背景"（粒度、衔接边界等）改为**真正的领域开发背景**（客户是谁 / 行业专业术语 / 常见约定）
  - 仅以 **SRM 为示例骨架**展示业务背景的组织形式
  - 明确"实际起草时根据用户描述补充对应领域的背景知识"
  - prd-writer 与 fs-writer 内容保持一致主干，仅在 FS 版本中追加了字段命名约定与通用表字段（与 FS 实施更相关）

## [0.3.1] - 2026-05-20

### Removed

- 删除 skill 目录下的 `README.md`（按 Anthropic 官方规范，SKILL.md 是唯一入口；skill 内不放独立 README）
  - `product-management/prd-writer/README.md`
  - `product-management/fs-writer/README.md`

### Changed

- 根 `README.md` 增强：补充每个 skill 的"适用场景 / 触发词 / 核心机制 / 输出"详情，弥补 skill README 删除后访客可能丢失的信息
- 两个 SKILL.md 的文件清单同步更新（去掉 README 行）

## [0.3.0] - 2026-05-20

### Changed

- **prd-writer：PRD §5 分解逻辑重构**
  - "能力组"概念替换为"**子模块**"，对应 §5.1 / §5.2 / ... 章节号
  - FR 编号改为**多级数字**：FR-1.1 / FR-1.2 / FR-2.1（前缀对应子模块号）
  - FR 字段从 6 个增至 7 个：新增**场景描述**（自由叙述用户场景与目标）
  - 明确"FR 即 User Story，但不强制 As-I want-So that 句式"
  - 默认 FS 拆分约定：一个子模块 = 一份 FS；紧耦合 FR 同处一子模块，自然合并到同一 FS
- **fs-writer：复杂逻辑组件位置调整**
  - 删除 `reference/complex-logic.md`（与 fs-template.md 内已有的 4 种工具示例重复）
  - SKILL.md 文件导航与 §5 章节直接指向 fs-template.md 内置示例
  - fs-writer 不再含 reference/ 子目录

### Removed

- prd-writer：旧的"能力组（Capability Group）"概念
- fs-writer：reference/complex-logic.md（内容已合并到 fs-template.md）

## [0.2.1] - 2026-05-20

### Changed

- **example/ 移动到 assets/example/**：例子本质是"模板的样例形态"，归 assets 子目录更自然
- **memory/lessons.md 收窄范围**：删除文件内的"历史修订记录"节；明确 memory 只放跨版本沉淀的**长期经验、教训、自检规则**，版本号修订日志归本 CHANGELOG
- 顶层 README 与各 skill SKILL.md 同步更新文件导航与目录树

## [0.2.0] - 2026-05-20

### Changed

- **重组两个 skill 为 6 目录标准结构**，便于渐进式加载：
  - `SKILL.md`（入口主文件，含文件导航）
  - `README.md`（人类安装文档）
  - `assets/`（输出模板）
  - `reference/`（按需加载的方法论）
  - `context/`（术语表 + 业务背景）
  - `example/`（典型产出片段示例）
  - `memory/`（长期教训库，每次起草前必读）
- SKILL.md 大幅瘦身：prd-writer 180 → 159 行；fs-writer 330 → 156 行
- 把"常见错误自检"从 SKILL.md 挪入 `memory/lessons.md`，作为长期教训库
- 顶层 README 更新结构说明，加入"渐进式加载设计"理念

### Added

- prd-writer 新增：reference/clarification-patterns.md（澄清问题高级模式）
- prd-writer 新增：context/glossary.md（术语表）
- prd-writer 新增：context/business-background.md（企业级软件背景）
- prd-writer 新增：example/srm-quotation-snippet.md（典型 PRD 片段）
- prd-writer 新增：example/clarification-batch.md（典型澄清问题批次）
- prd-writer 新增：memory/lessons.md（长期教训库）
- fs-writer 新增：reference/complex-logic.md（复杂逻辑表达手段）
- fs-writer 新增：context/glossary.md（术语表）
- fs-writer 新增：context/business-background.md（FS 受众与边界）
- fs-writer 新增：example/srm-quotation-snippet.md（典型 FS 片段）
- fs-writer 新增：example/credit-check-decision.md（复杂逻辑示例）
- fs-writer 新增：memory/lessons.md（长期教训库）

## [0.1.0] - 2026-05-20

### Added

- 初始化仓库结构：按场景分类（product-management/、未来可加 dev-tools/、marketing/ 等）
- 顶层文档：README、LICENSE (MIT)、CHANGELOG、.gitignore
- 新增 skill：**product-management/prd-writer** v1.0
  - 起草企业级 PRD（产品需求文档）
  - 8 节模板（核心 6 + 可选 2）
  - 6 字段 FR 格式
  - P0/P1 澄清机制 + Scope Exclusion + 业务实体边界
  - 两阶段渐进起草（v0.1 业务意图 + v1.0 完整版）
- 新增 skill：**product-management/fs-writer** v1.0
  - 从 PRD 功能点派生 FS（功能规格书）
  - 6 节模板（流程说明 → 功能概述 → 功能界面 → 关键字段说明 → 功能逻辑 → 数据表结构）
  - 4 种复杂逻辑表达手段（决策表 / 分支流程图 / 异常清单 / 算法说明）
  - 字段名中英双写、数据类型业务化（CHAR/NUM/DATE/ACL/勾选框/JSON）
  - 与 prd-writer 配套使用，形成 PRD → FS 协作链路
