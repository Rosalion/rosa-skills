# Changelog

本仓库整体的变更记录。各 skill 内部的细粒度变更记录在各自 `SKILL.md` 末尾的 CHANGELOG 块中。

## [Unreleased]

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
