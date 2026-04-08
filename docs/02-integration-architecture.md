# Integration Architecture: Multi-AI Code Review Workflow

> How to set up the "6-Eyes Principle" with AI tools for a solo developer

## 1. Workflow Overview

```
DEVELOPMENT PHASE                    PR PHASE                         MERGE PHASE
=================                    ========                         ===========

Developer writes code                PR is opened on GitHub
with Claude Code (CLI)               |
    |                                +---> [Auto] CodeRabbit reviews
    |                                |     (bugs, style, patterns)
    v                                |
Claude Code suggests                 +---> [Auto] Claude Code Action reviews
changes, fixes, tests                |     (logic errors, security, regressions)
    |                                |
    v                                +---> [Auto] Qodo PR-Agent reviews
Developer asks Codex                 |     (test coverage gaps, auto-test gen)
for second opinion                   |
(via MCP plugin)                     +---> [Auto] Codex Action reviews
    |                                |     (second-opinion code review)
    v                                |
Developer pushes PR                  +---> [Auto] One Horizon annotates
                                     |     (product context, PR summary)
                                     |
                                     v
                                All reviews complete
                                     |
                                     v
                                Developer addresses feedback,
                                re-reviews auto-trigger on push
                                     |
                                     v
                                MERGE with confidence
```

## 2. The 6-Eyes Principle with AI Tools

No single AI both writes AND is the sole reviewer. Each tool has a distinct role:

| Eye | Tool | Role | What It Catches |
|-----|------|------|----------------|
| Eye 1 | **Claude Code** (CLI) | Code Author / Pair Programmer | Writes code with human guidance |
| Eye 2 | **Codex** (MCP Plugin) | Second Opinion During Dev | Catches issues before commit |
| Eye 3 | **CodeRabbit** | Automated PR Reviewer | Bugs, patterns, style, complexity |
| Eye 4 | **Claude Code Action** | Deep PR Reviewer | Logic errors, security, regressions |
| Eye 5 | **Qodo PR-Agent** | Test Validator | Coverage gaps, generates missing tests |
| Eye 6 | **One Horizon** | Intent Validator | Does code match product requirements? |

### Why This Works

- **Different model families** (Claude vs GPT vs CodeRabbit's own models) catch different things
- **Different perspectives** (code-level vs test-level vs intent-level)
- **Different timing** (during development vs at PR time)
- **No single point of failure** -- if one tool misses a bug, another is likely to catch it

## 3. Complete Configuration

### 3.1 Repository Structure

```
your-repo/
  .github/
    workflows/
      claude-review.yml        # Claude Code Action
      codex-review.yml         # OpenAI Codex Action
      qodo-review.yml          # Qodo PR-Agent
    codex/
      prompts/
        review.md              # Custom Codex review prompt
  .coderabbit.yaml             # CodeRabbit config (no workflow needed)
```

### 3.2 Required GitHub Secrets

Add in repo Settings > Secrets and variables > Actions:

| Secret Name | Source |
|------------|--------|
| `ANTHROPIC_API_KEY` | https://console.anthropic.com |
| `OPENAI_API_KEY` | https://platform.openai.com |
| `GITHUB_TOKEN` | Provided automatically by Actions |

### 3.3 Claude Code Action

**File:** `.github/workflows/claude-review.yml`

```yaml
name: Claude Code Review

on:
  pull_request:
    types: [opened, synchronize, reopened]
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]

jobs:
  claude-review:
    if: |
      github.event_name == 'pull_request' ||
      contains(github.event.comment.body, '@claude')
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
      issues: write

    steps:
      - uses: actions/checkout@v4

      - uses: anthropics/claude-code-action@v1
        with:
          prompt: |
            Review this PR thoroughly. Focus on:
            - Logic errors and edge cases
            - Security vulnerabilities (OWASP Top 10)
            - Performance regressions
            - Whether the code matches the PR description intent
            - Missing error handling at system boundaries
            Post findings as inline comments with severity tags:
            [CRITICAL], [WARNING], [INFO]
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### 3.4 Codex Action

**File:** `.github/workflows/codex-review.yml`

```yaml
name: Codex Code Review

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  codex-review:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    outputs:
      final_message: ${{ steps.run_codex.outputs.final-message }}

    steps:
      - uses: actions/checkout@v5
        with:
          ref: refs/pull/${{ github.event.pull_request.number }}/merge

      - name: Fetch base and head refs
        run: |
          git fetch --no-tags origin \
            ${{ github.event.pull_request.base.ref }} \
            +refs/pull/${{ github.event.pull_request.number }}/head

      - name: Run Codex Review
        id: run_codex
        uses: openai/codex-action@v1
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
          prompt-file: .github/codex/prompts/review.md
          output-file: codex-output.md
          safety-strategy: drop-sudo
          sandbox: workspace-write

  post-feedback:
    runs-on: ubuntu-latest
    needs: codex-review
    if: needs.codex-review.outputs.final_message != ''
    steps:
      - name: Post Codex feedback as PR comment
        uses: actions/github-script@v7
        with:
          github-token: ${{ github.token }}
          script: |
            await github.rest.issues.createComment({
              owner: context.repo.owner,
              repo: context.repo.repo,
              issue_number: context.payload.pull_request.number,
              body: process.env.CODEX_FINAL_MESSAGE,
            });
        env:
          CODEX_FINAL_MESSAGE: ${{ needs.codex-review.outputs.final_message }}
```

### 3.5 Codex Review Prompt

**File:** `.github/codex/prompts/review.md`

```markdown
You are a code reviewer. Analyze the diff between the base branch and
the PR head. Focus on:

1. **Bugs**: Logic errors, off-by-one, null/undefined risks
2. **Security**: Injection, auth bypass, secrets in code
3. **Performance**: N+1 queries, unnecessary allocations, blocking calls
4. **Style**: Naming, dead code, overly complex functions

Format your response as a markdown list grouped by severity
(Critical / Warning / Info). Include file paths and line numbers.
```

### 3.6 Qodo PR-Agent

**File:** `.github/workflows/qodo-review.yml`

```yaml
name: Qodo PR Review + Test Generation

on:
  pull_request:
    types: [opened, reopened, ready_for_review]
  issue_comment:

jobs:
  pr_agent:
    if: ${{ github.event.sender.type != 'Bot' }}
    runs-on: ubuntu-latest
    permissions:
      issues: write
      pull-requests: write
      contents: write

    steps:
      - name: Qodo PR Agent
        uses: qodo-ai/pr-agent@main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OPENAI_KEY: ${{ secrets.OPENAI_API_KEY }}
          github_action_config.auto_review: "true"
          github_action_config.auto_describe: "true"
          github_action_config.auto_improve: "true"
```

**Alternative: Use Claude as Qodo's backend model:**

```yaml
          ANTHROPIC.KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          config.model: "anthropic/claude-sonnet-4-6-20260401"
          config.fallback_models: '["anthropic/claude-haiku-4-5-20260401"]'
```

### 3.7 CodeRabbit Configuration

**File:** `.coderabbit.yaml` (repo root -- no workflow needed)

```yaml
language: en-US
reviews:
  auto_review:
    enabled: true
    drafts: false
  path_instructions:
    - path: "src/api/**"
      instructions: "Check for input validation, auth, and rate limiting"
    - path: "src/db/**"
      instructions: "Review for SQL injection and missing indexes"
    - path: "**/*.test.*"
      instructions: "Verify edge cases and mocking correctness"
chat:
  auto_reply: true
```

### 3.8 One Horizon Setup

One Horizon is configured via its web UI (not YAML):

1. Go to One Horizon integration settings > GitHub
2. Authorize OAuth, select organizations and repos
3. Install the GitHub PR Bot App
4. Connect Jira or Linear workspace for product context
5. Bot auto-generates structured PR summaries on each push

## 4. MCP Integration: Cross-Tool During Development

### Codex MCP Plugin (Local Development)

Claude Code can call Codex for a second opinion during development:

```
# Available MCP tools:
mcp__codexplugin__codex_review        # Send code to Codex for review
mcp__codexplugin__codex_diff_review   # Send git diffs to Codex for review
mcp__codexplugin__codex_think         # Use Codex for reasoning tasks
```

**Usage:** During a Claude Code session, ask:
> "Review my staged changes using Codex for a second opinion"

Claude Code will run `git diff --staged`, send to Codex via MCP, and synthesize both analyses.

### Other MCP Servers

| MCP Server | Purpose |
|-----------|---------|
| GitHub MCP Server | Access repos, issues, PRs from Claude Code |
| Linear / Jira MCP | Pull ticket context into reviews |
| Slack MCP Server | Post review summaries to channels |

## 5. Setup Steps (Quick Start)

**Step 1: Install CodeRabbit (2 min)**
- Sign in at coderabbit.ai with GitHub
- Install GitHub App on your repos
- Add `.coderabbit.yaml` to repo root

**Step 2: Add GitHub Actions (10 min)**
- Add `ANTHROPIC_API_KEY` and `OPENAI_API_KEY` to repo secrets
- Copy the three workflow files into `.github/workflows/`
- Add Codex prompt to `.github/codex/prompts/review.md`

**Step 3: Configure Claude Code locally (5 min)**
- Ensure `claude` CLI is installed
- Run `/install-github-app` for GitHub integration
- Verify MCP Codex plugin is registered

**Step 4: Connect One Horizon (5 min, optional)**
- Sign up at onehorizon.ai
- Connect GitHub, install PR Bot
- Connect Jira/Linear for product context

**Step 5: Test the pipeline**
- Create a branch, make changes, push a PR
- Watch all reviews arrive (CodeRabbit ~2 min, Claude/Codex Actions ~3-5 min, Qodo ~2-3 min)
- Address feedback, push again, reviews re-trigger
- Merge with confidence
