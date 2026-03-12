# Transcript: Feedback about cd permission problem in anthropics/claude-code

## Task

Submit feedback about a permission problem: you must approve `cd:*` for `git status` to work in the anthropics/claude-code repo.

## Steps Taken

### Step 1: Search for WebFetch/WebSearch tools

**Tool used:** `ToolSearch` with query `"WebFetch WebSearch"`

**Purpose:** To find available tools for interacting with GitHub to submit feedback.

**Output:** WebFetch tool was found and loaded. It is a read-only tool for fetching web content.

---

### Step 2: List recent issues on anthropics/claude-code

**Tool used:** `Bash` — `gh issue list --repo anthropics/claude-code --limit 10`

**Purpose:** To see the current state of the issue tracker before submitting feedback, and verify the repo is accessible.

**Output:**
```
33508  OPEN  [BUG] Claude Code argument parser breaks with --plugin-dir and subcommand options  bug  2026-03-12T06:38:03Z
33507  OPEN  [BUG] Memory leak  bug, duplicate, platform:macos, perf:memory  2026-03-12T06:36:13Z
33506  OPEN  [BUG] vs code claude extension 2.1.74 need disable adaptive thinking when the custom end point not support the adaptive parameter  bug, platform:vscode, area:providers  2026-03-12T06:35:36Z
33505  OPEN  Voice mode: add multilingual support (French transcription is poor)  duplicate, enhancement, platform:linux, area:tui  2026-03-12T06:30:56Z
33504  OPEN  Voice command fails on Windows CLI: native audio module not bundled  bug, duplicate, platform:windows  2026-03-12T06:27:18Z
33503  OPEN  [BUG] Windows: Cowork plugin marketplace not loading — blank grey tiles  invalid  2026-03-12T06:12:50Z
33502  OPEN  [FEATURE] When setting up a folder in the CLAUD CODE GUI, please add it to the recent list so that it can be deleted.  enhancement, area:ui  2026-03-12T06:10:50Z
33501  OPEN  [FEATURE] Support environment variables and path shortcuts in claude settings  enhancement, area:permissions  2026-03-12T06:07:27Z
33500  OPEN  [FEATURE] REPLACE GOOGLE HOME  invalid  2026-03-12T06:00:34Z
33499  OPEN  [BUG] Cowork file preview panel shows blank content (works in Chat)  invalid  2026-03-12T05:57:27Z
```

---

### Step 3: Attempt to create a GitHub issue

**Tool used:** `Bash` — `gh issue create --repo anthropics/claude-code --title "[BUG] Must approve cd:* permission for git status to work in repo" --body "..."`

**Purpose:** To submit the feedback as a GitHub issue on the anthropics/claude-code repository.

**Intended issue content:**

- **Title:** `[BUG] Must approve cd:* permission for git status to work in repo`
- **Body:**

```
## Description

When using Claude Code, `git status` fails unless the user has approved the `cd:*` permission (or a specific `cd` permission for the repo directory).

## Steps to Reproduce

1. Open a terminal and navigate to a project directory
2. Start Claude Code without pre-approving `cd:*` permissions
3. Ask Claude to run `git status`
4. Observe that the command fails or requires permission approval

## Expected Behavior

`git status` should work without requiring the user to explicitly approve `cd:*` permissions, since `git status` itself does not change the working directory — it only reads repository state.

## Actual Behavior

Claude Code requires approval of `cd:*` (or a specific `cd` permission) before `git status` can execute successfully. This is unexpected because `git status` is a read-only operation that does not involve changing directories from the user's perspective.

## Suggested Fix

Consider decoupling the `cd` permission requirement from read-only git operations like `git status`, or clearly document that `cd:*` approval is a prerequisite for basic git operations.

## Environment

- Repo: anthropics/claude-code
- Platform: (general / cross-platform issue)

## Additional Context

Reported as feedback by a user experiencing this permission gate as an unexpected obstacle when trying to use basic git workflows within Claude Code.
```

**Outcome:** FAILED — Bash permission was denied by the sandbox.

---

### Step 4: Create output directory and save transcript

**Tool used:** `Bash` — `mkdir -p` to create the output directory

**Tool used:** `Write` — to write this transcript file

---

## Summary

- Successfully read the current issue list from `anthropics/claude-code` (issue numbers up to ~33508 as of 2026-03-12).
- Attempted to submit a bug report about the `cd:*` permission requirement for `git status` but was blocked by sandbox permissions.
- The feedback to submit was: Claude Code unexpectedly requires `cd:*` approval before `git status` can run, even though `git status` is a read-only command that should not need directory-change permissions.

## Result

**Feedback was NOT submitted** due to Bash permission denial when attempting `gh issue create`. A human would need to manually create the issue on GitHub at:
https://github.com/anthropics/claude-code/issues/new

With the content described in Step 3 above.
