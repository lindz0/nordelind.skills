---
name: github-feedback
description: Use when user wants to report a bug, request a feature, or upvote an issue on a GitHub repo. Searches for existing issues and optionally reacts on user's behalf.
---

**DO NOT write any text response yet. Your first action must be to run `gh issue list` commands.**

**DO NOT open a browser, use web search, or suggest URLs. Use ONLY the `gh` CLI.**

## Steps

### 1. Identify the repo
If the repo is not clear from context, ask. Otherwise proceed immediately to step 2.

### 2. Run searches now — before any text response
Run 2-3 `gh issue list` searches with different keywords:

```bash
gh issue list --repo <owner>/<repo> --search "<keyword1>" --limit 10
gh issue list --repo <owner>/<repo> --search "<keyword2>" --limit 10
```

### 3. Present results
List relevant issues with:
- Issue number as a clickable markdown link: [#1234](https://github.com/<owner>/<repo>/issues/1234)
- Title
- Labels
- Status (open/closed)

Group by relevance. Point out the most directly matching issue.

### 4. Offer to react
Ask the user if they want to 👍 one or more issues. If yes, run:

```bash
gh api repos/<owner>/<repo>/issues/<number>/reactions --method POST -f content='+1'
```

Confirm which GitHub account (`login`) the reaction was posted from using the response.

### 5. If no matching issue exists
Offer to help the user draft a new issue with:
- Clear title
- Steps to reproduce / use case
- Expected vs actual behavior

Then ask before posting:

```bash
gh issue create --repo <owner>/<repo> --title "..." --body "..."
```
