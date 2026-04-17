# bypass-aigc-detection

一个 [Perplexity Computer Agent Skill](https://www.perplexity.ai/computer/skills)，用于降低 AI 生成内容（AIGC）的检测率。

## 原理

本技能基于 [BypassAIGC](https://github.com/chi111i/BypassAIGC) 项目的逆向分析，提炼出其核心方法论：

### 核心思路

AI 检测工具（如 GPTZero、AIGC-X）识别的是 AI 文本的统计特征：
- 词汇选择的均匀性
- 句式结构的规范性
- 逻辑连接词的高频使用
- 特定"华丽词汇"的高频出现（nuanced, leverage, robust 等）

通过系统性地破坏这些特征，即可大幅降低检测率。

### 双阶段处理

1. **第一阶段：论文润色（Polish）** — 增加人类写作中常见的冗余表达、解释性短语和结构变化
2. **第二阶段：原创性增强（Enhance）** — 进一步消除残留 AI 特征，注入更强的"人类风格指纹"

### 核心技术

- **中文**：动词短语扩展、逻辑辅助词增强、系统性词汇替换、括号内容融合、句式微调
- **英文**：「英→中→中文结构优化→机械回译」范式 — 通过跨语言维度的转换，利用中文语法结构作为"模具"重塑英文文本的底层结构
- **智能分段**：按段落分割（≤500字/段），逐段处理，短段落自动跳过
- **上下文压缩**：已处理段落作为历史传递，超过阈值时自动压缩，保证全文风格一致

## 目录结构

```
bypass-aigc-detection/
├── SKILL.md                          # 主技能文件
└── references/
    ├── polish-prompt.md              # 第一阶段润色 Prompt 详细参考
    ├── enhance-prompt.md             # 第二阶段增强 Prompt 详细参考
    ├── emotion-prompt.md             # 感情文章改写 Prompt 参考
    └── architecture.md              # 系统架构参考
```

## 使用方式

1. 下载 `bypass-aigc-detection/` 目录
2. 打包为 zip 文件
3. 上传到 [Perplexity Computer Skills](https://www.perplexity.ai/computer/skills)
4. 在对话中提到"降低AIGC检测率"、"论文润色"、"降AI率"等关键词即可触发

## 致谢

- 原始项目：[chi111i/BypassAIGC](https://github.com/chi111i/BypassAIGC)
- 许可：CC BY-NC-SA 4.0（禁止商业使用）
