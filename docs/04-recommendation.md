# Final Recommendation

> For a 1-person AI-first company seeking highest code quality

## TL;DR

Use **Claude Code** as your primary development tool, with **Codex** as a second opinion via MCP. On every PR, let **CodeRabbit** (free), **Claude Code Action**, **Qodo PR-Agent**, and **One Horizon** (free) auto-review in parallel. This gives you 6 independent "eyes" at ~$30/mo.

## The Stack

### Primary Development: Claude Code ($20/mo Pro)
- Your daily pair programmer and coding agent
- Deep reasoning for complex architecture
- 1M context window for understanding large codebases
- Built-in code review capability for pre-commit checks

### Second Opinion During Dev: Codex via MCP ($0-5/mo API)
- Use the MCP plugin to get Codex's take on your code without leaving Claude Code
- Different model family = different failure modes = better coverage
- Especially useful before committing complex logic

### Automated PR Review Layer (runs in parallel on every PR):

| Tool | Cost | What It Does |
|------|------|-------------|
| **CodeRabbit** | $0 | First-pass bug/pattern/style review |
| **Claude Code Action** | ~$1-3/mo API | Deep logic, security, regression review |
| **Qodo PR-Agent** | ~$1-2/mo API | Test coverage gaps + auto-test generation |
| **Codex Action** | ~$1-2/mo API | Second-opinion review (different model) |
| **One Horizon** | $0 | Validates code matches product intent |

### Optional Add-ons

| Tool | Cost | When to Add |
|------|------|------------|
| GitHub Copilot Pro | $10/mo | If you want fast inline completions |
| Sourcery Pro | $12/mo | If you need security scanning |
| CodeRabbit Pro | $24/mo | If free tier rate limits become an issue |

## Why This Combination Works

### 1. Model Diversity
Claude (Anthropic) and Codex/GPT (OpenAI) have different training, architectures, and failure modes. A bug that Claude misses, GPT might catch -- and vice versa. CodeRabbit uses its own fine-tuned models. This diversity is the core strength.

### 2. Perspective Diversity
- **CodeRabbit** looks at code patterns and common bugs
- **Claude Code Action** reasons deeply about logic and security
- **Qodo** thinks about testability and coverage
- **One Horizon** checks alignment with business requirements
- **Codex** provides an independent second opinion

No single tool covers all five dimensions. Together, they form a comprehensive review.

### 3. Timing Diversity
- **During development:** Claude Code writes, Codex (MCP) pre-reviews
- **At PR time:** All five tools review in parallel
- **Post-merge:** One Horizon tracks delivery against requirements

### 4. Cost Efficiency
The entire stack runs at **~$25-35/mo** -- less than one hour of a human code reviewer. The free tiers of CodeRabbit, Qodo, and One Horizon are genuinely sufficient for a solo developer.

## The 4-Eyes vs 6-Eyes Decision

### Minimum Viable Quality (4 Eyes) -- ~$20/mo
1. You write code with Claude Code
2. CodeRabbit auto-reviews the PR (free)
3. Claude Code Action does deep review (~$2/mo)

This is sufficient for most projects. You get the author + two independent AI reviewers.

### Recommended Quality (6 Eyes) -- ~$30/mo
Add Codex (second opinion during dev), Qodo (test validation), and One Horizon (intent validation). This covers all major quality dimensions.

### Maximum Quality (8+ Eyes) -- ~$65/mo
Add Sourcery (security scanning), GitHub Copilot (additional completions), and upgrade CodeRabbit to Pro. Only needed for high-stakes systems.

## My Take

For a 1-person AI-first company:

1. **Start with the 4-eyes setup** ($20/mo). Get comfortable with the workflow.

2. **Upgrade to 6-eyes** when you're building features that matter to paying customers. The marginal cost (~$10/mo more) is trivial compared to the quality improvement.

3. **Never skip the PR step.** Even as a solo dev, always use branches and PRs. The automated review pipeline only works with PRs.

4. **Claude Code is your anchor tool.** It's where you spend 80% of your AI-assisted time. The other tools are the safety net around it.

5. **The Codex MCP bridge is underrated.** Getting a second opinion from a different AI model family during development -- before you even push -- catches issues that would otherwise only surface in PR review. This is your "shift left" strategy.

6. **One Horizon is most valuable if you use a task tracker.** If you're using Jira or Linear, connect it. If you're just coding ad-hoc, skip it for now and add it when you formalize your process.

7. **Budget for one human expert review per quarter** ($200-500). AI tools are excellent at catching bugs and patterns, but a senior architect reviewing your system design once per quarter is invaluable for strategic decisions AI tools can't make.

## Implementation Priority

1. **Week 1:** Set up Claude Code + CodeRabbit (free). Establish the PR workflow.
2. **Week 2:** Add Claude Code Action + Codex Action to GitHub Actions.
3. **Week 3:** Add Qodo PR-Agent. Set up Codex MCP plugin locally.
4. **Week 4:** Connect One Horizon (if using task tracker). Fine-tune review prompts based on initial feedback.

After the first month, you'll have a fully automated 6-eyes review pipeline that catches more issues than most small teams with human-only review.
