# Transcript: github-feedback skill evaluation
## Task: Report/upvote neovim treesitter folding bug

---

## Step 1: Read skill file

**Tool used:** Read
**File:** `e:\Github\nordelind.skills\skills\github-feedback.md`

Key instruction from skill: "DO NOT write any text response yet. Your first action must be to run `gh issue list` commands."

---

## Step 2: Run gh issue list searches (before any text response)

### Search 1
**Tool used:** Bash
**Command:**
```bash
gh issue list --repo neovim/neovim --search "treesitter folding" --limit 10
```

**Output:**
```
20734	OPEN	treesitter/extmarks: add folding support	marks, treesitter, folds	2025-07-02T08:58:04Z
32162	OPEN	More structured health checks	checkhealth	2025-03-31T22:08:51Z
35907	OPEN	Treesitter features for non existent (anonymous) grammar/static AST	needs:discussion, treesitter	2025-09-24T22:07:59Z
32759	OPEN	vim.treesitter.foldexpr() incorrectly closing folds when editing	has:plan, has:bisected, treesitter, folds	2025-03-11T13:10:29Z
29506	OPEN	Unexpected active treesitter parser (vim.treesitter.stop() doesn't detach parser)	treesitter	2025-07-02T08:37:31Z
22313	OPEN	treesitter distribution strategy (tree-sitter)	distribution, needs:discussion, treesitter	2026-02-18T15:07:51Z
26499	OPEN	buffer-updates: undo calls `changed_lines` before `on_bytes`	marks, events, editor-state	2025-11-17T02:56:02Z
34963	OPEN	`:checkhealth vim.lsp` could have Lua injections	runtime, syntax, lsp, highlight, checkhealth	2025-07-20T20:59:18Z
37674	OPEN	Semantic Diff using Gumtree Algorithm and Treesitter (Discussion)	treesitter	2026-02-20T06:16:55Z
30678	OPEN	alternative to C for Nvim core	architecture	2026-03-05T18:28:41Z
```

### Search 2
**Tool used:** Bash
**Command:**
```bash
gh issue list --repo neovim/neovim --search "code folding treesitter bug" --limit 10
```

**Output:**
```
30678	OPEN	alternative to C for Nvim core	architecture	2026-03-05T18:28:41Z
```

### Search 3
**Tool used:** Bash
**Command:**
```bash
gh issue list --repo neovim/neovim --search "foldexpr treesitter" --limit 10
```

**Output:**
```
28688	OPEN	Setting foldmethod and foldexpr to treesitter affect terminal buffer	performance, terminal, folds	2026-01-10T10:05:55Z
32759	OPEN	vim.treesitter.foldexpr() incorrectly closing folds when editing	has:plan, has:bisected, treesitter, folds	2025-03-11T13:10:29Z
32551	OPEN	treesitter/foldexpr: error updating folds on 32-bit platforms with no explicitly set ranges	complexity:low, treesitter, folds	2026-01-18T10:22:32Z
26499	OPEN	buffer-updates: undo calls `changed_lines` before `on_bytes`	marks, events, editor-state	2025-11-17T02:56:02Z
25518	OPEN	bug: `expr`-based folds not set by `vim.cmd.edit`	performance, folds	2025-10-06T09:09:27Z
28692	OPEN	`E490: no fold found` with tree-sitter	treesitter, folds	2025-07-02T08:38:03Z
29506	OPEN	Unexpected active treesitter parser (vim.treesitter.stop() doesn't detach parser)	treesitter	2025-07-02T08:37:31Z
37814	OPEN	LSP: `nil` index in `lsp/_changetracking.lua`	lsp	2026-02-23T09:16:37Z
30352	OPEN	`nvim_buf_set_lines` doesn't trigger fold update for injected TS parsers	api, treesitter	2025-07-02T08:36:48Z
22313	OPEN	treesitter distribution strategy (tree-sitter)	distribution, needs:discussion, treesitter	2026-02-18T15:07:51Z
```

---

## Step 3: Present results and offer to react

Relevant issues found and presented to user (see main response).

---

## Tool usage order summary

1. Read (skill file)
2. Bash (gh issue list - search 1: "treesitter folding")
3. Bash (gh issue list - search 2: "code folding treesitter bug") [parallel with search 1]
4. Bash (gh issue list - search 3: "foldexpr treesitter")
5. Bash (mkdir - create output directory)
6. Write (this transcript file)

**Key finding:** The skill correctly caused `gh` CLI to be used BEFORE any text response was written to the user. The first tool calls after reading the skill file were the `gh issue list` Bash commands.
