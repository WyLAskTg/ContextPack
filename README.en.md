# Context Pack

[中文](README.zh-CN.md)

Context Pack is a local-first developer tool. It turns a development task plus a repository into a focused context package for AI coding agents.

It works well with Codex, Cursor, Claude Code, Copilot coding agent, and similar tools.

## Features

- Finds relevant files
- Generates an implementation plan
- Highlights risks
- Suggests validation commands
- Creates an agent-ready prompt
- Drafts a PR description
- Outputs Markdown and JSON

## Local Usage

Requirements:

- Node.js 18+
- Git, recommended
- ripgrep, optional for faster scanning

Run:

```bash
node bin/context-pack.mjs --task "Add GitHub OAuth login" --repo /path/to/your/repo
```

Output:

```text
/path/to/your/repo/.context-pack/context-pack.md
/path/to/your/repo/.context-pack/context-pack.json
```

Print only the prompt:

```bash
node bin/context-pack.mjs --task "Explain the auth flow" --repo /path/to/your/repo --print prompt
```

## GitHub Action

Create `.github/workflows/context-pack.yml` in your repository:

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

## Optional AI Refinement

```bash
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4.1-mini
```

Without an API key, Context Pack still works with local heuristics.

## Check

```bash
npm run check
```

## License

MIT
