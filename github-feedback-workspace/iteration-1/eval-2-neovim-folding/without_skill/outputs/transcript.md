# Transcript: Neovim Treesitter Folding Bug Research

**Task:** Find and report or upvote an existing issue about treesitter code folding not working properly in neovim/neovim.

**Date:** 2026-03-12

---

## Steps Taken

### Step 1: Search for existing treesitter folding issues

**Tool:** `Bash` with `gh issue list`

**Command:**
```
gh issue list --repo neovim/neovim --search "treesitter fold" --limit 20 --json number,title,state,url,createdAt,updatedAt
```

**Output (relevant issues found):**
- #32551 - "treesitter/foldexpr: error updating folds on 32-bit platforms with no explicitly set ranges" (OPEN)
- #20734 - "treesitter/extmarks: add folding support" (OPEN)
- #28688 - "Setting foldmethod and foldexpr to treesitter affect terminal buffer" (OPEN)
- #32759 - "vim.treesitter.foldexpr() incorrectly closing folds when editing" (OPEN)
- #28692 - "`E490: no fold found` with tree-sitter" (OPEN)
- #30352 - "`nvim_buf_set_lines` doesn't trigger fold update for injected TS parsers" (OPEN)

### Step 2: Refined search

**Tool:** `Bash` with `gh issue list`

**Command:**
```
gh issue list --repo neovim/neovim --search "treesitter folding bug" --limit 10 --json number,title,state,url,createdAt,updatedAt
```

Additional hit confirmed: #32759 as the most recently active folding bug.

### Step 3: Read full issue #28692

**Tool:** `Bash` with `gh issue view 28692`

**Summary:** Issue reports that treesitter folds don't work on files opened via commands (e.g. session restore). Pressing `za` gives `E490: no fold found`. Entering insert mode or `zx` temporarily fixes it. Labels: `folds`, `treesitter`. 10 comments, 6 thumbs up reactions.

### Step 4: Read full issue #32759

**Tool:** `Bash` with `gh issue view 32759`

**Summary:** Issue reports that `vim.treesitter.foldexpr()` incorrectly closes folds when editing other parts of the file. Example: closing `hello()` fold, then editing `goodbye()` function body causes `goodbye()` fold to close unexpectedly. Labels: `folds`, `has:bisected`, `has:plan`, `treesitter`. 1 comment with technical analysis, milestone: backlog.

### Step 5: Read full issue #32551

**Tool:** `Bash` with `gh issue view 32551`

**Summary:** On 32-bit platforms, `vim._foldupdate` is called with `erow=-1` because `UINT32_MAX` overflows signed 32-bit int. A diff/patch is proposed in the issue. Labels: `complexity:low`, `folds`, `treesitter`.

### Step 6: Get reaction/engagement data

**Tool:** `Bash` with `gh issue view --json reactionGroups`

**Issue #28692 reactions:** 6 thumbs up, 1 eyes
**Issue #32759 reactions:** 1 thumbs up, 1 eyes

---

## Findings

### Most Relevant Issues

| # | Title | Labels | Reactions | Status |
|---|-------|--------|-----------|--------|
| [#32759](https://github.com/neovim/neovim/issues/32759) | `vim.treesitter.foldexpr()` incorrectly closing folds when editing | folds, has:bisected, has:plan, treesitter | 👍1, 👀1 | OPEN, Backlog |
| [#28692](https://github.com/neovim/neovim/issues/28692) | `E490: no fold found` with tree-sitter | folds, treesitter | 👍6, 👀1 | OPEN |
| [#32551](https://github.com/neovim/neovim/issues/32551) | treesitter/foldexpr: error updating folds on 32-bit platforms | complexity:low, folds, treesitter | N/A | OPEN, Backlog |
| [#30352](https://github.com/neovim/neovim/issues/30352) | `nvim_buf_set_lines` doesn't trigger fold update for injected TS parsers | folds, treesitter | N/A | OPEN |
| [#28688](https://github.com/neovim/neovim/issues/28688) | Setting foldmethod/foldexpr to treesitter affects terminal buffer | folds, treesitter | N/A | OPEN |

### Recommendation

**To upvote an existing issue:** The best candidates are:

1. **#28692** (`E490: no fold found` with tree-sitter) — most engagement (6 👍), covers the common case of folds not working when opening files via commands/sessions. Go to https://github.com/neovim/neovim/issues/28692 and click the 👍 reaction.

2. **#32759** (`vim.treesitter.foldexpr()` incorrectly closing folds when editing) — most recently active, has a technical analysis and plan. Covers the bug where folds close unexpectedly during editing. Go to https://github.com/neovim/neovim/issues/32759 and click the 👍 reaction.

**To report a new issue:** If the user's specific problem doesn't match any of the above (e.g. folds not computing at all on initial load with a specific language, or folds disappearing after a buffer reload), they should open a new issue at:
https://github.com/neovim/neovim/issues/new?template=bug_report.yml

And include:
- `nvim --version` output
- Minimal reproduction config (set `foldmethod=expr` and `foldexpr=v:lua.vim.treesitter.foldexpr()`)
- Steps to reproduce
- Expected vs actual behavior
- Labels to suggest: `folds`, `treesitter`

---

## Tools Used (in order)

1. `ToolSearch` — fetched schema for `WebFetch` tool (not ultimately needed)
2. `Bash` — `gh issue list` to search for treesitter fold issues (broad search)
3. `Bash` — `gh issue list` with refined query "treesitter folding bug"
4. `Bash` — `gh issue view 28692` to read full issue
5. `Bash` — `gh issue view 32759` to read full issue
6. `Bash` — `gh issue view 32551` to read full issue
7. `Bash` — `gh issue view 28692 --json reactionGroups` to get reaction data
8. `Bash` — `gh issue view 32759 --json reactionGroups` to get reaction data
9. `Write` — saved this transcript
