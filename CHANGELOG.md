# Changelog

本仓库整体的变更记录。各 skill 内部的细粒度变更记录在各自 `SKILL.md` 末尾的 CHANGELOG 块中。

## [Unreleased]

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
