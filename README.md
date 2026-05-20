# rosa-skills

Rosa 的 Claude Code skill 集合。按场景分类组织，每个 skill 独立可用。

## 仓库结构

```
rosa-skills/
├── README.md             ← 本文件
├── LICENSE               ← MIT
├── CHANGELOG.md          ← 仓库级变更日志
├── .gitignore
└── product-management/   ← 场景：产品经理工作流
    ├── prd-writer/       ← 起草企业级 PRD
    │   ├── SKILL.md      ← 入口主文件（精简 ~160 行）
    │   ├── README.md     ← 人类安装文档
    │   ├── assets/       ← 模板 + 示例
    │   │   ├── prd-template.md
    │   │   └── example/  ← 典型产出片段
    │   ├── reference/    ← 按需加载的规则与方法论
    │   ├── context/      ← 术语表 + 业务背景
    │   └── memory/       ← 长期教训库（每次起草前必读）
    └── fs-writer/        ← 起草功能规格书 (FS)
        ├── SKILL.md
        ├── README.md
        ├── assets/
        │   ├── fs-template.md
        │   └── example/
        ├── reference/
        ├── context/
        └── memory/
```

每个 skill 采用统一的 **5 目录结构**（SKILL.md + README.md + 4 个子目录），便于渐进式加载：

- **SKILL.md**：入口规则 + 工作流概览 + 文件导航
- **assets/**：输出模板（起草时复制填空）+ `example/` 子目录（典型产出片段）
- **reference/**：复杂场景的方法论（按需加载，简单场景不读）
- **context/**：术语表与业务背景（用户输入不足时按需补常识）
- **memory/**：长期教训库（仅放跨版本沉淀的经验、教训、自检规则；版本号修订请进顶层 CHANGELOG）

未来可能新增的场景目录：`dev-tools/`、`marketing/`、`research/` 等。

## Skills 一览

### product-management

| Skill | 一句话定位 | 触发词 |
|---|---|---|
| **prd-writer** | 把模糊的客户需求 / 会议纪要 / RFP 整理成结构化 PRD（业务契约层）| "写 PRD"、"draft PRD"、"起草需求文档" |
| **fs-writer** | 把 PRD 中的功能点派生为开发可直接实施的 FS（实现契约层）| "写 FS"、"draft FS"、"起草 F-NNN" |

> **prd-writer + fs-writer 配套使用**，形成"PRD → FS → 开发"闭环。详见各 skill 自带的 README。

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
├── SKILL.md              ← Claude Code 主入口，含 frontmatter + 工作流 + 文件导航
├── README.md             ← 给人类读的安装与使用说明
├── assets/               ← 输出模板骨架 + 示例
│   ├── <skill>-template.md   ← 模板（起草时复制填空）
│   └── example/              ← 典型产出片段（不确定格式时参考）
├── reference/            ← 按需加载的规则与方法论（复杂场景才读）
├── context/              ← 术语表 + 业务背景常识（输入不足时按需读）
└── memory/               ← 长期教训库（每次起草前必读，沉淀实战经验）
```

**渐进式加载设计**：SKILL.md 只保留入口规则与文件导航；详细方法论、术语、示例都放在子目录，按场景需求才加载，避免一次性把所有信息塞给模型。

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
