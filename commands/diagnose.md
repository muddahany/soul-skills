---
name: diagnose
description: Health-check all soul-skills installed in ~/.claude/skills/. Reports which skills are present, whether SOUL is populated, which platform hats exist, when files were last modified, and flags anything stale (>6 months) or missing required state. Triggers on /diagnose, "check my soul-skills", "are my skills outdated", "what state is my voice setup in", "audit my skills".
---

# Soul-Skills Diagnose

This command audits the state of soul-skills on the user's machine and reports back a clean status table.

## Steps

### 1. Check ~/.claude/skills/ exists

```bash
ls ~/.claude/skills/ 2>/dev/null
```

If the directory does not exist, tell the user no soul-skills are installed and point them at the install instructions.

### 2. For each known soul-skills component, check status

Loop through these expected components:

- `deslop` (universal)
- `soul` (personalised core)
- `whisper-flow` (input pipeline, listens to you)
- `read-incoming` (input pipeline, listens to others)
- `platform-hat-deriver` (meta-skill)
- `voice-hat-template` (manual escape hatch)
- `platform-hat-template` (manual escape hatch)

For each, check:

- Does `~/.claude/skills/<name>/SKILL.md` exist?
- File modification date.
- For `soul` specifically: does the file contain the "STATE CHECK" callout? If yes, SOUL is unpopulated.

### 3. Scan for derived platform hats

```bash
ls ~/.claude/skills/ | grep -E "-hat$" | grep -v "voice-hat-template\|platform-hat-template"
```

Examples: `linkedin-hat`, `reddit-hat`, `slack-hat`, etc.

For each, check modification date.

### 4. Flag staleness

For any skill where the SKILL.md is older than 6 months from today, mark it `[stale]` with the date.

### 5. Output a status table

Use this format:

```
## soul-skills health report

| Skill | Status | Last touched |
|---|---|---|
| deslop | Installed | YYYY-MM-DD |
| soul | Installed, POPULATED / UNPOPULATED | YYYY-MM-DD |
| platform-hat-deriver | Installed / Missing | YYYY-MM-DD |
| whisper-flow | Installed / Missing | YYYY-MM-DD |
| voice-hat-template | Installed / Not installed | YYYY-MM-DD |
| platform-hat-template | Installed / Not installed | YYYY-MM-DD |

## Derived platform hats

| Hat | Last touched | Notes |
|---|---|---|
| linkedin-hat | YYYY-MM-DD | [stale if >6 months] |
| reddit-hat | YYYY-MM-DD | |
| ... | | |

## Issues found

- [If SOUL is unpopulated]: Your SOUL skill is not populated. Run `/soul` to start the onboarding.
- [If platform-hat-deriver missing but SOUL is populated]: You have a populated SOUL but no deriver installed. Run `/plugin install platform-hat-deriver@soul-skills` to enable hat derivation.
- [If any skill is stale]: <skill-name> has not been touched in N months. Consider reviewing.
- [If no derived hats]: You have not derived any platform hats yet. After SOUL is populated, say "create a [LinkedIn/Reddit/etc] hat for me".

## Recommendations

- [Concrete next steps based on what's missing or stale]
```

### 6. Be honest about uncertainty

If you cannot tell whether something is populated (e.g., a hat exists but you cannot verify it has real content), say so. Do not guess.

## When NOT to use

- User is currently in the middle of SOUL onboarding. Wait until it completes.
- User has not installed soul-skills at all. There is nothing to diagnose.
