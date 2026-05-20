# prd-writer

Claude Code skill：起草或迭代企业级 PRD（产品需求文档）。按"摘要 → 业务上下文 → 业务流程 → 业务实体 → 功能点列表 → 范围"6 节顺序，两阶段渐进式输出。

**配套使用**：与 [fs-writer](https://github.com/Rosalion/rosa-skills/tree/main/product-management/fs-writer) 协作。PRD 输出 FR-NNN 列表，fs-writer 派生 FS。

## 适用场景

- B2B / 企业级软件（ERP / SRM / MES / WMS / CRM 等）的需求文档撰写
- 从模糊的客户访谈、邮件、RFP 整理为结构化 PRD
- 团队需要"PRD → FS → 实施"的清晰交付链
- 适合中小型项目（一个 PRD 一个模块；超大模块需拆多个 PRD）

## 安装

### 方式 1：手动安装（推荐）

1. 解压本压缩包，得到 `prd-writer/` 文件夹
2. 将 `prd-writer/` 文件夹复制到 Claude Code 的 skills 目录：

   ```bash
   # macOS / Linux
   cp -r prd-writer ~/.claude/skills/

   # Windows (PowerShell)
   Copy-Item -Recurse prd-writer $env:USERPROFILE\.claude\skills\
   ```

3. 重启 Claude Code（或新开一个对话），即可使用

### 方式 2：项目级安装

```bash
mkdir -p <project-dir>/.claude/skills/
cp -r prd-writer <project-dir>/.claude/skills/
```

## 验证安装

在 Claude Code 中说："写 PRD" 或 "draft PRD for XXX"，应当能触发本 skill。

## 使用

直接说出意图，例如：

- "帮我写一份 SRM 报价模块的 PRD"
- "draft PRD for client X's WMS"
- "起草需求文档：基于这份会议纪要"
- "把这个 RFP 整理成 PRD"

Skill 会按以下流程引导：

1. **Step 0**：识别输入、确认 PRD 覆盖范围
2. **Step 1**：P0/P1 一批澄清问题（必含范围排除追问）
3. **Step 2**：起草 v0.1 业务意图（§1 摘要、§2 业务上下文、§3 业务流程、§4 业务实体）
4. **Step 3**：审阅通过后起草 v1.0（§5 功能点列表、§6 范围）
5. **Step 4**：询问是否追加 §7 待决问题 / §8 备注（默认不要）

## PRD 8 节模板

| 节 | 内容 | 必选 |
|---|---|---|
| §1 摘要 | 业务背景、目标、核心价值 | ✅ |
| §2 业务上下文 | 问题陈述、目标用户、为什么是现在 | ✅ |
| §3 业务流程 | Mermaid flowchart，多流程多图 | ✅ |
| §4 业务实体 | 实体清单（不写字段）+ ER 图 | ✅ |
| §5 功能点列表 | FR-NNN 按能力组分组，每条 6 字段 | ✅ |
| §6 范围 | 范围内 / 范围外 / 未来扩展 | ✅ |
| §7 待决问题 | OQ-NNN | 🟡 可选 |
| §8 备注 | 关键约束、依赖、假设 | 🟡 可选 |

## FR 的 6 字段格式

```markdown
### FR-001 <祈使句标题>
- **优先级**：P0 / P1 / P2
- **用户角色**：<谁触发或受益>
- **业务规则**：
  1. <规则 1>
  2. <规则 2>
- **验收标准**：
  - 给定 X，当 Y 时，则 Z
- **依赖/备注**：<可选>
```

## 核心写作规范

### PRD 该写什么 ✅

- 业务背景与痛点
- 业务流程（动作 + 决策点）
- 业务实体（概念层，不写字段）
- 功能点列表（业务规则 + 验收标准）
- 范围内 / 范围外 / 未来扩展

### PRD 不该写什么 ❌

- **不写字段级 schema**（VARCHAR(200)、DECIMAL(10,2)…） → 留给 FS
- **不写 API 路径 / HTTP method** → 留给 FS
- **不写错误码** → 留给 FS（错误**提示文案**可在业务规则里写）
- **不写技术选型**（PostgreSQL / Redis 等）
- **不写界面原型 / ASCII 线框** → 留给 FS

## 核心高价值机制

| 机制 | 价值 |
|---|---|
| **P0/P1 澄清** | P0 必答、P1 带默认值；用户 2-3 分钟答完，避免阻塞起草 |
| **Scope Exclusion 必含** | §6 范围外至少 5 项，避免范围蔓延 |
| **业务实体 vs 字段边界** | PRD 不写字段，与 FS 边界清晰 |
| **两阶段渐进起草** | v0.1 业务意图先确认方向，再写 v1.0 完整版 |
| **PRD → FS 衔接** | FR-NNN 是 fs-writer 的输入；末尾可附"给 FS 起草者的提示" |

## 与 fs-writer 的协作

```
prd-writer 产出 PRD
   ├── §3 业务流程  ──→  fs-writer §1 流程说明
   ├── §4 业务实体  ──→  fs-writer §6 数据表结构（FS 才落字段）
   ├── §5 功能点    ──→  fs-writer 派生 FS（每个 FR 或一组相关 FR = 一份 FS）
   └── §6 范围      ──→  fs-writer 判断 FS 是否在范围内
```

## 文件清单

- `SKILL.md` — Skill 主文件（Claude Code 读取）
- `_template.md` — PRD 模板骨架（8 节）
- `README.md` — 本文件（安装说明）

## 致谢

本 skill 整合了：
- 知微行易 SRM / DxERP 真实项目实践
- Anthropic 的 tob-prd skill 方法论参考
- 多轮起草迭代过程中提炼的"P0/P1 澄清"、"Scope Exclusion"、"业务实体边界"等高价值机制

## 版本

v1.0 — 2026-05-19
