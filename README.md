# rosa-skills

Rosa 的 Claude Code skill 集合。按场景分类组织，每个 skill 独立可用。

## 仓库结构

```
rosa-skills/
├── README.md             ← 本文件（仓库唯一的 README，供人类访客阅读）
├── LICENSE               ← MIT
├── CHANGELOG.md          ← 仓库级变更日志
├── .gitignore
├── product-management/   ← 场景：产品经理工作流
│   ├── prd-writer/       ← 起草企业级 PRD
│   │   ├── SKILL.md      ← Claude Code 入口主文件
│   │   ├── assets/       ← 模板 + 示例
│   │   │   ├── prd-template.md
│   │   │   └── example/  ← 典型产出片段
│   │   ├── reference/    ← 按需加载的规则与方法论
│   │   ├── context/      ← 术语表 + 业务背景
│   │   └── memory/       ← 长期教训库（每次起草前必读）
│   └── fs-writer/        ← 起草功能规格书 (FS)
│       ├── SKILL.md
│       ├── assets/
│       │   ├── fs-template.md   ← 内置 4 种复杂逻辑工具的骨架示例
│       │   └── example/
│       ├── context/
│       └── memory/
│       # 注：fs-writer 无 reference/ 子目录（复杂逻辑工具已内置在 fs-template.md）
└── subagents/            ← Reviewer 团队（被主 skill 调度的 review subagent）
    ├── business-analyst/ ← 业务分析师视角 review PRD
    │   ├── SKILL.md
    │   ├── context/
    │   └── memory/
    ├── architect/        ← 架构师视角 review PRD
    │   └── （同结构）
    └── qa/               ← QA 视角 review PRD
        └── （同结构）
```

每个 skill 采用 Anthropic 官方推荐的标准结构：**SKILL.md 作为唯一入口，无独立 README**。需要人类阅读的安装、使用说明都在本仓库根 README 里。

- **SKILL.md**：Claude Code 入口；含 frontmatter（name / description / triggers）+ 工作流 + 文件导航
- **assets/**：输出模板（起草时复制填空）+ `example/` 子目录（典型产出片段）
- **reference/**：复杂场景的方法论（按需加载，简单场景不读）
- **context/**：术语表与业务背景（用户输入不足时按需补常识）
- **memory/**：长期教训库（仅放跨版本沉淀的经验、教训、自检规则；版本号修订请进顶层 CHANGELOG）

未来可能新增的场景目录：`dev-tools/`、`marketing/`、`research/` 等。

## Skills 一览

### product-management

**prd-writer + fs-writer 配套使用**，形成"PRD → FS → 开发"闭环。

#### prd-writer

- **定位**：把模糊的客户需求 / 会议纪要 / RFP 整理成结构化 PRD（业务契约层）
- **适用场景**：B2B / 企业级软件（ERP / SRM / MES / WMS / CRM 等）的需求文档撰写
- **触发词**："写 PRD"、"draft PRD"、"起草需求文档"、"帮我整理需求"、"client X 的 PRD"
- **核心机制**：P0/P1 澄清 → 8 节模板 → 7 字段 FR → 子模块分组 + 多级编号 → 范围排除追问
- **输出**：含 §1 摘要、§2 业务上下文、§3 业务流程（Mermaid）、§4 业务实体、§5 功能点列表（FR-1.1 / FR-2.1 ...）、§6 范围

#### fs-writer

- **定位**：把 PRD 中的功能点派生为开发可直接实施的 FS（实现契约层）
- **适用场景**：从 PRD 派生功能规格书，给开发团队实施；前后端一体化项目尤其适合
- **触发词**："写 FS"、"draft FS"、"针对 XX 功能点写规格"、"起草 F-NNN"
- **核心机制**：分段渐进 → 6 节模板 → 字段中英双写 + 业务类型 → 4 种复杂逻辑表达手段（决策表 / 分支流程图 / 异常清单 / 算法说明）
- **输出**：含 §1 流程说明、§2 功能概述、§3 功能界面（含 ASCII 原型）、§4 关键字段说明、§5 功能逻辑（步骤表）、§6 数据表结构

### subagents

**Reviewer 团队**：被主 skill 调度的 review subagent，**不直接面向用户**，而是由 prd-writer 在 Step 3.5 并行 spawn 来评审 PRD 草稿。用户可在 prd-writer Step 0 选择是否启用本团队。

| Subagent | 视角 | 5 个 review 维度 |
|---|---|---|
| **business-analyst-reviewer** | 业务可行性 / 用户价值 | 用户价值清晰度、业务流闭环、范围合理性、FR 覆盖完整性、业务规则完整性 |
| **architect-reviewer** | 技术可行性 / 演进性 | 技术可行性、与现有系统兼容、数据模型合理性、性能与扩展性、演进性与扩展点 |
| **qa-reviewer** | 可测性 / 边界完整性 | 验收标准可测性、边界场景覆盖、异常分支完整性、状态机测试覆盖、跨 FR 一致性 |

每个 subagent 输出结构化 review 报告（✅ 通过 / ⚠️ 建议 / ❌ 必改 三档），主 prd-writer 汇总后由用户裁决采纳哪些。

## 安装某个 skill

每个 skill 是独立的目录，复制到 Claude Code 的 skills 目录即可：

```bash
# macOS / Linux
cp -r product-management/prd-writer ~/.claude/skills/
cp -r product-management/fs-writer ~/.claude/skills/

# Windows (PowerShell)
Copy-Item -Recurse product-management\prd-writer $env:USERPROFILE\.claude\skills\
Copy-Item -Recurse product-management\fs-writer $env:USERPROFILE\.claude\skills\
```

重启 Claude Code 即可使用。

## 安装全部 skills

```bash
# macOS / Linux
for dir in product-management/*/; do
  cp -r "$dir" ~/.claude/skills/
done
```

## 一个 skill 长什么样（标准结构）

```
<skill-name>/
├── SKILL.md              ← Claude Code 主入口（唯一文档入口，无独立 README）
│                            含 frontmatter（name / description / triggers）+ 工作流 + 文件导航
├── assets/               ← 输出模板骨架 + 示例
│   ├── <skill>-template.md   ← 模板（起草时复制填空）
│   └── example/              ← 典型产出片段（不确定格式时参考）
├── reference/            ← 按需加载的规则与方法论（复杂场景才读，可选）
├── context/              ← 术语表 + 业务背景常识（输入不足时按需读）
└── memory/               ← 长期教训库（每次起草前必读，沉淀实战经验）
```

**渐进式加载设计**：SKILL.md 只保留入口规则与文件导航；详细方法论、术语、示例都放在子目录，按场景需求才加载，避免一次性把所有信息塞给模型。

**为什么 skill 目录下不放 README？** 按 Anthropic 官方规范，SKILL.md 是 Claude Code 唯一识别的入口；额外的 README 对模型不可见、对人类访客也是冗余（仓库级 README 已足够）。本仓库严格遵循此约定。

**memory/ 的范围界定**：仅放跨版本沉淀的**长期经验、教训、自检规则**。版本号修订日志归仓库根 `CHANGELOG.md`，不混在 memory 里。

## 设计哲学

- **极简优先** — 单个 skill 控制在 200-300 行内；多了反而成为枷锁
- **场景驱动** — 按真实工作场景分类（产品/开发/营销...），而非按技术类型
- **分段渐进** — 复杂任务分多步交付，每步留 checkpoint，避免一次大返工
- **业务可读 + 技术精确** — 字段中英双写、数据类型业务化、业务规则用完整中文句
- **不臆造** — 输入未明确的不写到输出；遇到边界拒绝外推

## 协作贡献

本仓库目前是私有的个人 skill 库。如有协作或反馈意向，欢迎提 issue 或 PR。

## License

[MIT](./LICENSE)
