# AI Code Review & QA Strategy

> Multi-tool approach for a 1-person AI-first company to ensure highest quality code through the "6-eyes principle"

## Repository Structure

```
docs/
  01-market-research.md          # Tool-by-tool analysis with pricing (10 tools)
  02-integration-architecture.md # How tools work together (workflows, configs)
  03-cost-analysis.md            # Cost breakdown and recommended setups
  04-recommendation.md           # Final recommendation and rationale
  05-persona-based-testing.md    # AI persona simulation for user journey QA
  06-codex-review-feedback.md    # Codex's critical review of this strategy
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

## The 8-Eyes Principle

| Eye | Tool | Role |
|-----|------|------|
| 1 | **Claude Code** (CLI) | Code Author / Pair Programmer |
| 2 | **Codex** (MCP Plugin) | Second Opinion During Development |
| 3 | **CodeRabbit** | Automated PR Review (bugs, patterns, style) |
| 4 | **Claude Code Action** | Deep PR Review (logic, security, regressions) |
| 5 | **Qodo PR-Agent** | Test Validator (coverage gaps, auto-test gen) |
| 6 | **One Horizon** | Intent Validator (does code match requirements?) |
| 7 | **Persona Testing** (Claude + Playwright) | Real user experience simulation |
| 8 | **Multi-persona diversity** | Edge cases across user types |

## Quick Start

See [docs/02-integration-architecture.md](docs/02-integration-architecture.md) for full setup instructions.

## Monthly Cost Estimate

| Setup | Cost | Tools |
|-------|------|-------|
| Budget | ~$10/mo | Copilot Pro + free tiers |
| Recommended | ~$30-44/mo | Claude Code Pro + Copilot Pro + free tiers |
| Premium | ~$64-84/mo | Full paid stack |

See [docs/03-cost-analysis.md](docs/03-cost-analysis.md) for detailed breakdown.

## Codex Review

This entire strategy was reviewed by OpenAI Codex (o4-mini + gpt-4.1) for gaps and risks. Key findings:
- **3-stage funnel** recommended over flat 6-eyes (fast gate -> deep review -> release)
- **Missing dimensions:** security scanning (Snyk/CodeQL), API contract testing, a11y, load testing
- **Cost underestimate:** budget $75-100/mo, not $30-50/mo
- **Biggest risk:** over-automation creating false confidence

See [docs/06-codex-review-feedback.md](docs/06-codex-review-feedback.md) for full review.
