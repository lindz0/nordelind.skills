# Benchmark: github-feedback skill — Iteration 1

## Summary

| Configuration | Pass Rate | Avg Tokens | Avg Duration |
|--------------|-----------|------------|--------------|
| with_skill   | **100%** (12/12) | 13,787 | 61.1s |
| without_skill | **33%** (4/12) | 19,743 | 79.8s |

**Delta: +67 percentage points** with skill vs without.

---

## Per-eval results

### Eval 0: cd permission / anthropics/claude-code

| Assertion | with_skill | without_skill |
|-----------|-----------|---------------|
| uses_gh_cli | ✅ | ✅ |
| searches_before_text | ✅ | ❌ |
| presents_markdown_links | ✅ | ❌ |
| offers_to_react | ✅ | ❌ |
| **Pass rate** | **4/4** | **1/4** |

### Eval 1: slow startup / microsoft/vscode

| Assertion | with_skill | without_skill |
|-----------|-----------|---------------|
| uses_gh_cli | ✅ | ✅ |
| searches_before_text | ✅ | ❌ |
| presents_markdown_links | ✅ | ❌ |
| offers_to_react | ✅ | ❌ |
| **Pass rate** | **4/4** | **1/4** |

### Eval 2: treesitter folding / neovim/neovim

| Assertion | with_skill | without_skill |
|-----------|-----------|---------------|
| uses_gh_cli | ✅ | ✅ |
| searches_before_text | ✅ | ❌ |
| presents_markdown_links | ✅ | ✅ |
| offers_to_react | ✅ | ❌ |
| **Pass rate** | **4/4** | **2/4** |

---

## Analyst observations

1. **`uses_gh_cli` passes for both** — The subagents know about gh CLI and use it regardless of skill. This assertion is non-discriminating in this eval setup. In real Claude Code sessions (with browser tools available), the baseline would likely fail here too — as seen in the user's manual tests.

2. **`searches_before_text` is the clearest discriminator** — Without the skill, agents always start with ToolSearch for WebFetch (their default habit). The skill's "DO NOT write any text response yet" instruction changes this order reliably.

3. **`offers_to_react` is the second clearest discriminator** — Without the skill, agents either skip reacting entirely, try to react without asking, or give raw commands for the user to run themselves. The skill makes Claude ask first and offer to do it on the user's behalf.

4. **`presents_markdown_links` almost passes without skill** — Baseline eval 2 used proper markdown links. This assertion may be too easy and doesn't differentiate well.

5. **Real-world gap is likely larger** — These evals ran in isolated subagents without browser MCP tools. The user's actual tests (with Playwright browser MCP loaded) showed Claude trying to open Chrome. The skill is especially important in sessions with browser tools available.
