[English](README.md)

# 论文检查 Prompt

一个用于通过 [Claude Code](https://docs.anthropic.com/en/docs/claude-code)（或任何 LLM 编程助手）检查学术 ML 论文的 meta prompt。由 [Zhuang Liu](https://liuzhuang13.github.io/) 开发。

## 这是什么

一个 prompt，指导 LLM 编程助手系统性地按照全面的写作和图表标准检查你的论文。助手会：

1. 下载并阅读最新的 [Figure & Table Guide](https://github.com/zlab-princeton-internal/figure-guide) 和 [Writing Guide](https://github.com/zlab-princeton-internal/wiki)
2. 将每条规则分类为 Python 可检查或仅 LLM 可检查
3. 编写并运行 Python 脚本进行自动检查
4. 使用 LLM 判断进行视觉、语义和结构检查（同时双重检查 Python 结果）
5. 通过 web search 验证所有引用
6. 生成中英双语报告，按颜色标记严重程度

因为助手在运行时才读取指南，所以即使指南更新了，这个 prompt 仍然有效。

## 如何使用

### 方式 A：复制粘贴 prompt

1. 打开 Claude Code（或你常用的 LLM 编程助手）
2. 将 [`PROMPT.md`](PROMPT.md)（中文）或 [`PROMPT_EN.md`](PROMPT_EN.md)（英文）的内容复制到对话中
3. 告诉它你的 Overleaf 项目文件夹路径

### 方式 B：保存为自定义命令

将 `PROMPT.md` 或 `PROMPT_EN.md` 保存为 Claude Code 自定义命令（例如 `~/.claude/commands/check-paper.md`），然后用 `/check-paper /path/to/project` 调用。

## 文件

| 文件 | 语言 | 说明 |
|------|------|------|
| [`PROMPT.md`](PROMPT.md) | 中文 | 完整的 meta prompt（中文版） |
| [`PROMPT_EN.md`](PROMPT_EN.md) | 英文 | 完整的 meta prompt（英文版） |

## 检查什么

Prompt 引用两份外部指南，定义了全部检查规则：

- **[Figure & Table Guide](https://github.com/zlab-princeton-internal/figure-guide)** — 矢量格式、字体、颜色、边框、箭头、排版、折线图、图表、caption
- **[Writing Guide](https://github.com/zlab-princeton-internal/wiki)** — 结构、语言、引用、claim、段落长度、appendix 标准、项目整洁

助手在运行时读取这些指南并自行制定检查计划，因此指南的任何更新都会自动反映。

## 输出

- `PAPER_CHECK_REPORT.md` — 完整的中英双语报告（详细程度完全相同）
- `PAPER_CHECK_REPORT.pdf` — 宽页面 PDF 版本

每个问题都包含一个从论文中引用的**可搜索字符串**，你可以直接 Ctrl+F 找到。

## 环境要求

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 或任何能读文件和跑 Python 的 LLM 编程助手
- Python 3.9+
- 含 `.tex` 和 `.bib` 文件的 LaTeX 项目
- 互联网（用于引用验证）
- pandoc + xelatex（可选，用于生成 PDF 报告）

## 许可证

MIT
