# Context Pack

Context Pack 可根据开发任务和本地代码仓库，生成一份给 AI 编程助手使用的上下文包。

可配合Codex、Cursor、Claude、Copilot等工具使用。

### 它会生成：

- 相关文件列表
- 实现计划
- 风险点
- 推荐验证命令
- 可直接复制给 AI coding agent 的 Prompt
- PR 描述草稿
- Markdown 和 JSON 输出

### 使用方式

要求：

- Node.js 18+
- Git，推荐
- ripgrep，可选，扫描更快

运行：

```bash
node bin/context-pack.mjs --task "Add GitHub OAuth login" --repo /path/to/your/repo
```

输出文件：

```text
/path/to/your/repo/.context-pack/context-pack.md
/path/to/your/repo/.context-pack/context-pack.json
```

只打印 Prompt：

```bash
node bin/context-pack.mjs --task "Explain the auth flow" --repo /path/to/your/repo --print prompt
```

### GitHub Action

在其他仓库中创建 `.github/workflows/context-pack.yml`：

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

      - uses: your-github-name/context-pack@v1
        with:
          comment-pr: true
```

## English

Context Pack is a local-first developer tool. It turns a development task plus a repository into a focused context pack for AI coding agents.

It works well with Codex, Cursor, Claude Code, Copilot coding agent, and similar tools.

### What It Generates

- Relevant files
- Implementation plan
- Risk notes
- Suggested validation commands
- Agent-ready prompt
- PR description draft
- Markdown and JSON outputs

### Local Usage

Requirements:

- Node.js 18+
- Git, recommended
- ripgrep, optional for faster scanning

Run:

```bash
node bin/context-pack.mjs --task "Add GitHub OAuth login" --repo /path/to/your/repo
```

Output files:

```text
/path/to/your/repo/.context-pack/context-pack.md
/path/to/your/repo/.context-pack/context-pack.json
```

Print only the prompt:

```bash
node bin/context-pack.mjs --task "Explain the auth flow" --repo /path/to/your/repo --print prompt
```

Without an API key, Context Pack still works with local heuristics.

### GitHub Action

Create `.github/workflows/context-pack.yml` in another repository:

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

      - uses: your-github-name/context-pack@v1
        with:
          comment-pr: true
```
