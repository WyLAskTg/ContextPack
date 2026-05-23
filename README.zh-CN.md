# Context Pack

[English](README.en.md)

Context Pack 是一个本地优先的开发者工具。它会根据“开发任务 + 代码仓库”，生成一份给 AI 编程助手使用的上下文包。

适合配合 Codex、Cursor、Claude Code、Copilot coding agent 等工具使用。

## 功能

- 找出相关文件
- 生成实现计划
- 标出风险点
- 推荐验证命令
- 生成可复制给 AI coding agent 的 Prompt
- 生成 PR 描述草稿
- 输出 Markdown 和 JSON

## 本地使用

要求：

- Node.js 18+
- Git，推荐
- ripgrep，可选，扫描更快

运行：

```bash
node bin/context-pack.mjs --task "Add GitHub OAuth login" --repo /path/to/your/repo
```

输出：

```text
/path/to/your/repo/.context-pack/context-pack.md
/path/to/your/repo/.context-pack/context-pack.json
```

只打印 Prompt：

```bash
node bin/context-pack.mjs --task "Explain the auth flow" --repo /path/to/your/repo --print prompt
```

## GitHub Action

在你的仓库中创建 `.github/workflows/context-pack.yml`：

```yaml
name: Context Pack

on:
  pull_request:

permissions:
  contents: read
  issues: write

jobs:
  context-pack:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: WyLAskTg/context-pack@v1
        with:
          comment-pr: true
```

## 可选 AI 增强

```bash
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4.1-mini
```

没有 API key 时，Context Pack 也能用本地启发式生成。

## 检查

```bash
npm run check
```

## 许可证

MIT
