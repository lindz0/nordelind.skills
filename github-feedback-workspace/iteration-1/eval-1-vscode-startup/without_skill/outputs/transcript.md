# Transcript: Finding and Upvoting VSCode Slow Startup Issues

**Task:** Find issues about slow startup time in microsoft/vscode and upvote one if it exists.

**Date:** 2026-03-12

---

## Steps Taken

### Step 1: Create output directory
**Tool:** Bash
**Command:** `ls "E:\Github\nordelind.skills\github-feedback-workspace\iteration-1\eval-1-vscode-startup\without_skill\outputs" 2>/dev/null || mkdir -p "..."`
**Result:** Directory created successfully.

---

### Step 2: Search for issues about slow startup time
**Tool:** Bash
**Command:** `gh issue list --repo microsoft/vscode --search "slow startup time" --limit 20 --json number,title,url,reactions,state`
**Result:** Error - "reactions" is not a valid JSON field. Available field is "reactionGroups".

---

### Step 3: Search with correct fields
**Tool:** Bash
**Command:** `gh issue list --repo microsoft/vscode --search "slow startup time" --limit 20 --json number,title,url,reactionGroups,state`
**Result:** Found 20 issues. Most relevant ones:

| # | Title | State | Thumbs Up |
|---|-------|-------|-----------|
| 192493 | Slow startup time on 1.82.0 | OPEN | 3 |
| 204243 | slow start up | OPEN | 8 |
| 193948 | Slow startup in version 1.82 | OPEN | 0 |
| 192766 | Startup takes over 30 seconds, with or without extensions | OPEN | 1 |
| 262472 | Perf: showing Chat view on startup is slow | OPEN | 1 |

---

### Step 4: Search with more specific terms
**Tool:** Bash
**Command:** `gh issue list --repo microsoft/vscode --search "startup slow performance" --limit 10 --json number,title,url,reactionGroups,state`
**Result:** Found additional issues, including:
- #248664: VSCode is unresponsive on startup (OPEN, 0 reactions)
- #192493: Slow startup time on 1.82.0 (OPEN, 3 thumbs up)
- #193948: Slow startup in version 1.82 (OPEN, 0 reactions)

---

### Step 5: View details of issue #192493
**Tool:** Bash
**Command:** `gh issue view 192493 --repo microsoft/vscode --json number,title,url,reactionGroups,state,body,createdAt`
**Result:** Full details retrieved.

- **Title:** Slow startup time on 1.82.0
- **URL:** https://github.com/microsoft/vscode/issues/192493
- **State:** OPEN
- **Created:** 2023-09-07
- **Thumbs Up:** 3
- **Description:** With all extensions disabled, VS Code 1.82.0 takes 4x more time to start than VS Code 1.81.1, due to a slow renderer. Includes detailed performance marks showing regression in `window.loadUrl() => begin to require(workbench.desktop.main.js)` (320ms vs 2619ms) and `init storage` (27ms vs 1034ms).

---

### Step 6: View details of issue #204243
**Tool:** Bash
**Command:** `gh issue view 204243 --repo microsoft/vscode 2>&1 | head -30`
**Result:**

- **Title:** slow start up
- **State:** OPEN
- **Labels:** chromium, gpu, upstream
- **Assignee:** deepak1556
- **Comments:** 15
- **Description:** VS Code 1.86 opens slowly compared to previous versions. Windows 11, 12th Gen Intel i5.

---

### Step 7: Attempt to upvote issue #192493
**Tool:** Bash
**Command:** `gh api repos/microsoft/vscode/issues/192493/reactions --method POST --field content="+1"`
**Result:** PERMISSION DENIED — Bash tool access was denied for this operation.

---

## Summary

**Issues Found:** Yes, multiple issues about slow startup time exist in microsoft/vscode.

**Most Relevant Issues:**
1. **#192493** - "Slow startup time on 1.82.0" (https://github.com/microsoft/vscode/issues/192493) — Detailed regression report with performance profiling data. Open, 3 upvotes.
2. **#204243** - "slow start up" (https://github.com/microsoft/vscode/issues/204243) — Reports slow startup since version 1.86, assigned to a developer, 8 upvotes.
3. **#192766** - "Startup takes over 30 seconds, with or without extensions" (https://github.com/microsoft/vscode/issues/192766) — Extreme startup delay.

**Upvote Attempted:** Issue #192493 was selected for upvoting (most technically detailed and well-documented startup regression). The upvote command was prepared:
```
gh api repos/microsoft/vscode/issues/192493/reactions --method POST --field content="+1"
```
However, the Bash tool permission was denied before the upvote could be executed.

**Recommended action for user:** To upvote, visit https://github.com/microsoft/vscode/issues/192493 and click the thumbs-up reaction, or run:
```
gh api repos/microsoft/vscode/issues/192493/reactions --method POST --field content="+1"
```

---

## Tools Used (in order)

1. ToolSearch — to fetch WebFetch and WebSearch tool schemas
2. Bash — `mkdir -p` to create output directory
3. Bash — `gh issue list` (first attempt, wrong field name)
4. Bash — `gh issue list` (corrected with reactionGroups)
5. Bash — `gh issue list` (second search with different terms)
6. Bash — `gh issue view 192493` (detailed view with JSON)
7. Bash — `gh issue view 204243` (detailed view with head)
8. Bash — `gh api` to POST reaction (DENIED)
9. Write — to write this transcript
