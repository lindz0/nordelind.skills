---
name: github-feedback
description: Use when user wants to report a bug, request a feature, or upvote an issue on a GitHub repo. Searches for existing issues and optionally reacts on user's behalf.
---

## When to use
User mentions a problem with a tool, library, or project hosted on GitHub and wants to give feedback or upvote an issue.

## Steps

### 1. Identify the repo
Ask the user which GitHub repo (e.g. `anthropics/claude-code`) if not already clear from context.

### 2. Search for existing issues
Run 2-3 searches with different keywords to find related issues:

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
