# nordelind.skills

Personal Claude Code skills library.

## Install

```bash
claude plugin marketplace add github:lindz0/nordelind.skills
claude plugin install nordelind-skills
```

## Update

```bash
claude plugin update nordelind-skills@lindz0
```

## Kör en skill från terminalen

Skills laddas inte automatiskt i `-p`-läge. Skicka in skill-instruktionerna explicit via `--system-prompt`:

```bash
claude -p "Visa motorsportschema på Viaplay för kommande helg" \
  --allowedTools "WebFetch,WebSearch" \
  --system-prompt "$(cat ~/.claude/plugins/cache/lindz0/nordelind-skills/1.0.2/skills/viaplay-sport/SKILL.md)" \
  --output-format text
```

### Schemalagt jobb (PowerShell / Task Scheduler)

```powershell
claude -p "Visa motorsportschema på Viaplay för kommande helg" --allowedTools "WebFetch,WebSearch" --system-prompt (Get-Content "$env:USERPROFILE\.claude\plugins\cache\lindz0\nordelind-skills\1.0.2\skills\viaplay-sport\SKILL.md" -Raw) --output-format text
```
