# ✍️ bypass-aigc-detection

降低 AIGC 检测率的文本改写 Agent Skill —— 输入 AI 生成的论文或文章，通过双阶段改写 + 跨语言结构重塑，输出具有"人类写作印记"的文本。支持中英文。

An Agent Skill that rewrites AI-generated text to reduce AIGC detection rates. Two-stage rewriting pipeline with cross-lingual structural reshaping. Supports Chinese and English.

遵循 [Agent Skills 开放标准](https://agentskills.io)，兼容 Claude Code、Cursor、GitHub Copilot、Codex、Windsurf、Gemini CLI、Perplexity Computer 等 30+ AI Agent 平台。

## 安装 / Install

```bash
npx skills add Ficere/bypass-aigc-detection
```

> 需要 Node.js。安装后 Agent 会自动发现并按需加载该技能。
>
> Requires Node.js. Once installed, your agent will auto-discover and load this skill when relevant.

<details>
<summary>其他安装方式 / Alternative methods</summary>

**手动安装 / Manual install：**

```bash
git clone https://github.com/Ficere/bypass-aigc-detection.git
# 将整个目录复制到你的 Agent 的 skills 目录下即可
# Copy the directory to your agent's skills folder:
#   Claude Code:  ~/.claude/skills/
#   Cursor:       .cursor/skills/
#   Copilot:      .github/skills/
#   Codex:        ~/.codex/skills/
#   Gemini CLI:   .gemini/skills/
```

**Perplexity Computer：**

下载本仓库 zip → 在 [Skills 管理页面](https://www.perplexity.ai/computer/skills) 上传。

</details>

## 使用 / Usage

安装后直接用自然语言触发，无需任何配置：

```
帮我降低这篇论文的 AIGC 检测率
```

```
这段文字 AI 味太重了，帮我改得像人写的
```

```
Humanize this paragraph to bypass GPTZero detection
```

```
帮我润色一下这篇感情散文，风格要自然口语化
```

## 功能 / Features

| 功能 | 说明 |
|------|------|
| **双阶段改写** | 润色（Polish）→ 原创性增强（Enhance），两阶段叠加效果远优于单阶段 |
| **中文改写** | 动词短语扩展、逻辑辅助词增强、系统性词汇替换、括号内容融合 |
| **英文改写** | 「英→中→中文结构优化→机械回译」范式，利用中文语法结构重塑英文底层结构 |
| **智能分段** | 按段落自动分割（≤500 字/段），短段落（标题等）自动跳过 |
| **上下文压缩** | 已处理段落作为历史传递，超阈值自动压缩，保证全文风格一致 |
| **感情文章模式** | 中文混沌口语流 + 英文"愤世嫉俗专家"风格，适用于非学术类文章 |

<details>
<summary>处理模式一览 / Processing modes</summary>

| 模式 | 说明 | 阶段 |
|------|------|------|
| `paper_polish_enhance` | 论文润色 + 增强（默认，效果最好） | Polish → Enhance |
| `paper_polish` | 仅论文润色（改动较小） | Polish |
| `paper_enhance` | 仅原创性增强（直接增强原文） | Enhance |
| `emotion_polish` | 感情文章改写（非学术风格） | Emotion Polish |

</details>

<details>
<summary>核心原理 / How it works</summary>

AI 检测工具（GPTZero、AIGC-X 等）识别的是 AI 文本的统计特征：词汇选择的均匀性、句式结构的规范性、逻辑连接词的高频使用、特定"华丽词汇"的高频出现（nuanced, leverage, robust 等）。

本技能通过系统性破坏这些特征来降低检测率：

**中文策略（Protocol A）：**
- "处理" → "对…进行处理"，"实现" → "得以实现"
- "通过" → "借助"，"使用" → "运用"，"和" → "以及"
- 括号内容融合进句子，"把"字句替换"将"字句

**英文策略（Protocol B）—— 跨语言结构重塑：**
1. 英→中转译：按中文表达习惯转为中文
2. 中文结构优化：执行 Protocol A 润色规则
3. 机械式回译：逐字翻译回英文，严格保留中文语序
4. 最终英文带有源自中文逻辑的"异质感"

回译铁律：结构绝对优先（忠于中文词序），词汇基础化（规避 AI 高频词）。

</details>

<details>
<summary>改写示例 / Examples</summary>

**中文：**

原文：
> 本系统基于 Django 框架开发，使用了 RESTful API 进行前后端通信，通过 JWT 实现了用户认证。

改写后：
> 本系统是以 Django 框架为基础来开展相关的开发工作的，选用了 RESTful API 来进行前端以及后端之间的通信交互，凭借 JWT 得以实现了用户认证方面的功能。

**English：**

Original:
> The system leverages a microservices architecture to achieve high scalability and robust fault tolerance.

Rewritten:
> This system is by using microservices architecture to achieve high scalability and strong fault tolerance.

</details>

## 目录结构 / Structure

```
bypass-aigc-detection/
├── SKILL.md                   # 技能入口（Agent 自动读取）
├── references/
│   ├── polish-prompt.md       # 第一阶段润色 Prompt
│   ├── enhance-prompt.md      # 第二阶段增强 Prompt
│   ├── emotion-prompt.md      # 感情文章改写 Prompt
│   └── architecture.md        # 系统架构与流程参考
└── examples/
    ├── chinese-academic-paper.md   # 中文学术论文示例（paper_polish_enhance）
    ├── english-academic-paper.md   # 英文学术论文示例（paper_polish_enhance）
    └── chinese-emotion-article.md  # 中文感情文章示例（emotion_polish）
```

## 致谢 / Credits

核心方法论提炼自 [chi111i/BypassAIGC](https://github.com/chi111i/BypassAIGC)。

## License

[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — 禁止商业使用 / Non-commercial use only.
