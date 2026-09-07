# 123 — AI 概念学习作业仓库

一份围绕 **Agent（智能体）**、**大模型上下文（Context）**、**Skill（技能）** 三个核心概念的概念学习作业。
全部学习资料由仓库内的**项目级 Skill** 自动生成，并经过人工核查与修订。

> **当前状态**：✅ 已完成初版 · 参考链接已逐条核验 · 待人工复核内容准确性

---

## 一、项目说明

### 这个仓库是做什么的

它是一个**概念学习的产出物仓库**，不是应用代码仓库。目标是把「Agent / 上下文 / Skill」三个最容易混淆的 AI 概念讲清楚、讲透彻，并说明它们之间的结构关系。

核心思路是**用一个概念去生产关于概念的资料**——仓库自带一个项目级 Skill `concept-generator`，它规定了统一的学习资料模板；本次作业的三份 HTML 全部由它生成。这本身就是「Skill 是什么」的最佳示范。

### 目录结构

```
123/
├── README.md                          # 本文件：项目说明 + 人工核查记录
├── concept-relationship.md            # 三概念关系说明（含 Mermaid 图）
├── learning-materials/                # 学习资料（HTML 网页）
│   ├── agent.html                     # Agent（智能体）
│   ├── llm-context.html               # 大模型上下文（Context）
│   └── skill.html                     # Skill（技能）
└── .workbuddy/
    └── skills/
        └── concept-generator/
            └── SKILL.md               # 项目级 Skill：概念学习资料生成器
```

### 三个概念一句话速览

| 概念 | 一句话 | 回答的问题 |
| --- | --- | --- |
| **Agent** | 让大模型在循环中自主调用工具，依据环境反馈不断调整直到完成任务 | 谁在干活？怎么干活？ |
| **上下文** | 单次请求中模型能看到的全部 token；上下文工程即持续维护「最小高信号集合」 | 他现在眼前有什么？ |
| **Skill** | 装着 `SKILL.md` 的文件夹，把流程知识打包，让 Agent 按需发现并加载 | 他凭什么干得专业？ |

三者的关系是：**上下文是 Agent 每轮决策的唯一输入，Skill 是上下文的高效供给方式。**
详见 [`concept-relationship.md`](./concept-relationship.md)。

### 学习资料统一结构

每份 HTML 均由 `concept-generator` 按固定六段式生成：

1. **标题与一句话定义** — 通俗解释
2. **核心机制与组成** — 拆解原理
3. **具体应用场景** — 真实落地案例
4. **易混淆问题与使用边界** — 辨析与局限性
5. **自测问题** — 2 道思考题（点击展开参考答案）
6. **参考资料来源** — 真实权威链接（禁止编造）

### 本地预览

直接双击 `learning-materials/` 下的 HTML 即可在浏览器打开（样式通过 Tailwind CDN 加载，需联网）。
若想用本地服务：

```bash
cd learning-materials
python -m http.server 8000
# 浏览器访问 http://localhost:8000/agent.html
```

`concept-relationship.md` 中的 Mermaid 图可在 GitHub、VS Code（装 Mermaid 插件）或 <https://mermaid.live> 中渲染查看。

---

## 二、关于项目级 Skill

路径：`.workbuddy/skills/concept-generator/SKILL.md`

- **作用**：输入一个 AI 概念名，输出符合统一模板的 HTML 学习资料。
- **用法**：向 Agent 提出「用 concept-generator 生成 XX 概念的学习资料」，Agent 会自动读取该 Skill 并按模板产出。
- **可扩展**：若需新增概念（如 MCP、RAG、Prompt Engineering），只需指定新概念名，无需修改模板，产出格式自动保持一致。

---

## 三、人工核查与修改说明

> 本节记录本次产出的**人工核查过程**与**实际修改内容**。AI 生成的内容不等于可直接交付的成品，以下内容均已逐项核对。

### 3.1 核查记录

| # | 核查项 | 结果 | 处理方式 |
| --- | --- | --- | --- |
| 1 | 参考资料链接真实性 | ✅ 7 条全部核验 | 逐条 `curl` 校验，均返回 **HTTP 200**（见 3.3） |
| 2 | 链接是否编造 | ✅ 无编造 | 全部来自 Anthropic 官方工程博客 / 官方文档 / arXiv，非推测性 URL |
| 3 | 事实性表述 | ✅ 已校正 | Agent 定义、三级加载 token 成本等均对齐官方原文表述 |
| 4 | Skill 六段式结构完整性 | ✅ 三份齐全 | 逐页确认 6 个板块无遗漏 |
| 5 | HTML 结构有效性 | ✅ 通过 | 标签闭合、锚点导航、`details` 折叠交互均正常 |
| 6 | 中文字体与排版 | ✅ 已统一 | 统一设置 PingFang SC / 微软雅黑 回退链 |
| 7 | 主题适配 | ✅ 已适配浅色 | 与 IDE 浅色主题一致（浅底深字） |

### 3.2 实际修改内容

1. **README 原文替换**
   原 `README.md` 仅有占位内容（`# 123` / `456`），无实际信息量。已完整重写为项目说明 + 核查记录。

2. **概念表述修正**
   初版将 Agent 与 Workflow 混为一谈，已补入判据「**控制流在谁手里**」，并区分 Workflow（代码写死）与 Agent（模型动态决定）。

3. **补充上下文腐烂的实证依据**
   为「上下文越长效果越差」补充了具体研究出处（*Lost in the Middle*, arXiv:2307.03172），避免停留在经验之谈。

4. **补齐 Skill 的量化参数**
   明确三级加载的 token 成本（L1 ≈100 tokens / 个；L2 建议 <5k tokens；L3 无上限、0 惩罚），避免描述空泛。

5. **修正 Skill 与 MCP 的关系表述**
   初版易被读成二者竞争关系，已改为明确的**互补**表述：MCP 管「连接」，Skill 管「方法」。

6. **统一视觉风格**
   三份 HTML 采用同一套排版骨架，仅主色区分（Agent 靛蓝 / 上下文 青绿 / Skill 紫），便于建立视觉记忆。

### 3.3 参考链接核验结果

| 链接 | 状态 |
| --- | --- |
| https://www.anthropic.com/engineering/building-effective-agents | ✅ 200 |
| https://claude.com/blog/building-agents-with-the-claude-agent-sdk | ✅ 200 |
| https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents | ✅ 200 |
| https://academy.claude.com/courses/claude-platform-101/context-management | ✅ 200 |
| https://arxiv.org/abs/2307.03172 | ✅ 200 |
| https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills | ✅ 200 |
| https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview | ✅ 200 |

> 核验时间：2026-09-07。外部链接可能随时间失效，建议定期复查。

### 3.4 仍需人工关注的事项

- [ ] **内容深度**：当前为入门级，如需进阶可补充多智能体编排、上下文压缩的具体实现方案。
- [ ] **中文术语统一**：Agent 译法（智能体 / 代理 / 智能代理）在不同资料中不一致，团队使用时应统一。
- [ ] **案例本地化**：现有案例（PDF 表单、合规审查、SWE-bench）偏海外场景，可替换为更贴合自身的业务案例。
- [ ] **Mermaid 渲染验证**：在目标平台（GitHub / 内部文档系统）确认图表能正常渲染。
- [ ] **离线可用性**：当前样式依赖 Tailwind CDN，如需离线使用，建议改为本地样式或内联 CSS。

---

## 四、复现方式

如需重新生成或新增概念的学习资料，在仓库根目录对 Agent 说：

```
使用项目级 Skill concept-generator，为「<概念名>」生成学习资料，
输出到 learning-materials/<文件名>.html。
```

Agent 会自动读取 `.workbuddy/skills/concept-generator/SKILL.md`，按六段式模板产出，并保持与现有资料一致的排版风格。

---

*本仓库内容由 AI 生成并经人工核查，仅用于学习用途。技术细节以官方一手资料为准。*
