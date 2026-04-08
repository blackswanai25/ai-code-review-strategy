# AI Code Review & QA Strategy

> Multi-tool approach for a 1-person AI-first company to ensure highest quality code through the "6-eyes principle"

## Repository Structure

```
docs/
  01-market-research.md          # Tool-by-tool analysis with pricing
  02-integration-architecture.md # How tools work together (workflows, configs)
  03-cost-analysis.md            # Cost breakdown and recommended setups
  04-recommendation.md           # Final recommendation and rationale
.github/
  workflows/
    claude-review.yml            # Claude Code Action for PR review
    codex-review.yml             # OpenAI Codex Action for PR review
    qodo-review.yml              # Qodo PR-Agent for test coverage + review
  codex/
    prompts/
      review.md                  # Custom Codex review prompt
.coderabbit.yaml                 # CodeRabbit auto-review config
```

## The 6-Eyes Principle

| Eye | Tool | Role |
|-----|------|------|
| 1 | **Claude Code** (CLI) | Code Author / Pair Programmer |
| 2 | **Codex** (MCP Plugin) | Second Opinion During Development |
| 3 | **CodeRabbit** | Automated PR Review (bugs, patterns, style) |
| 4 | **Claude Code Action** | Deep PR Review (logic, security, regressions) |
| 5 | **Qodo PR-Agent** | Test Validator (coverage gaps, auto-test gen) |
| 6 | **One Horizon** | Intent Validator (does code match requirements?) |

## Quick Start

See [docs/02-integration-architecture.md](docs/02-integration-architecture.md) for full setup instructions.

## Monthly Cost Estimate

| Setup | Cost | Tools |
|-------|------|-------|
| Budget | ~$10/mo | Copilot Pro + free tiers |
| Recommended | ~$30-44/mo | Claude Code Pro + Copilot Pro + free tiers |
| Premium | ~$64-84/mo | Full paid stack |

See [docs/03-cost-analysis.md](docs/03-cost-analysis.md) for detailed breakdown.
