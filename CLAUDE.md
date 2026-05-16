# CLAUDE.md

> **For Claude Code:** This is an onboarding instructions file. The user has pointed you at this repo because they want to install one or more skills into their own Claude Code configuration. Follow the steps below. Read the file fully before acting.

## What this repo contains

| Path | Type | Role |
|---|---|---|
| `skills/deslop/` | Universal skill | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/soul/` | Personalized skill, populated via onboarding | Encodes the user's personal voice, writing style, and values that shape voice. Drives all "write as me" use cases. **Recommended core skill.** |
| `skills/platform-hat-deriver/` | Meta-skill | Auto-generates platform-specific hats from a populated SOUL plus a platform name. Built-in syntax reference for LinkedIn, Reddit, Slack, Twitter/X, Discord, GitHub, Substack, email (no user input needed for syntax). Only personal/contextual rules are asked. Run once per platform. |
| `skills/voice-hat-template/` | Manual template, escape hatch | Raw skeleton with placeholders. Only for users who want manual control instead of the SOUL onboarding. |
| `skills/platform-hat-template/` | Manual template, escape hatch | Raw skeleton for platform rules. Most users should prefer `platform-hat-deriver`. |

## Core thesis (state this to the user before anything else)

These skills AMPLIFY a genuine voice. They do not generate one from nothing. Before walking the user through onboarding, set the expectation explicitly:

- SOUL only works if the inputs are GENUINE. AI-generated writing samples or vague interview answers produce a generic AI-flavored soul that defeats the purpose.
- Effort is required. Done well, the SOUL setup takes 20 to 40 minutes. Do not rush.
- If typing is slow for the user, recommend voice-to-text (Wispr Flow, macOS Dictation, Whisper, or anything similar). Speaking surfaces authentic phrasing that typed answers smooth over.
- Using AI to STRUCTURE your real thoughts is productive. Using AI to GENERATE content from nothing is laziness and produces slop. This repo is for the first, not the second.

Tell the user this in your own words at the start of the session so they know what they are signing up for.

## Your job when the user lands here

1. **Greet the user briefly** and tell them what is available. State the core thesis above. Suggest the recommended path: install `deslop` + populate `soul`. Mention the manual template path exists if they ask.
2. **Confirm their choice and their readiness.** If they are in a rush, suggest they come back later. Half-effort SOUL is worse than no SOUL.
3. **Install `deslop`** with a straight `cp -r`. No customisation needed.
4. **Populate `soul`** using the onboarding flow below. This is the high-leverage step.
5. **Verify everything is in place** and tell them what to do next.

## Two install methods

You have two ways to install `deslop` and the templates:

1. **Plugin marketplace** (cleanest if Claude Code supports it for the user). Tell the user they can run `/plugin marketplace add muddahany/soul-skills` then `/plugin install deslop@soul-skills` (and similarly for `voice-hat-template`, `platform-hat-template`). Only use this for the non-SOUL skills, because SOUL needs the interactive onboarding flow below.
2. **Direct cp -r from the cloned repo**. Use this for SOUL (which you populate interactively before installing) and as a fallback if plugin marketplace install does not work.

## Standard install location

- macOS / Linux: `~/.claude/skills/`
- Windows: `%USERPROFILE%\.claude\skills\`

Always install into the user's home directory unless they explicitly ask for project-local.

```bash
mkdir -p ~/.claude/skills
```

## Step 1: install deslop (no customisation)

```bash
cp -r skills/deslop ~/.claude/skills/
```

That's it. `deslop` works as-is.

## Step 2: SOUL onboarding (the high-leverage step)

`soul` is the user's personal voice skill. It ships UNPOPULATED but is **self-onboarding**: the full interactive onboarding flow lives in `skills/soul/references/onboarding.md`. Load that file and run it end to end.

The onboarding covers:
- **Genuineness gate**: confirm user is ready to commit 20-40 minutes; recommend voice-to-text.
- **Mode selection**: sample, interview, or hybrid. User picks. No default.
- **Sample mode**: 5-10 real writing examples → pattern extraction.
- **Interview mode**: 13 questions about voice, style, values.
- **Hybrid**: sample first, interview fills gaps.
- **Drafting**: populate Identity, Voice rules, Writing style, Values, Examples sections.
- **Review iteration**: show draft, accept corrections.
- **Install**: overwrite `~/.claude/skills/soul/SKILL.md` with the populated version.

When the user says "set up my SOUL" or just runs `/soul` after installing the plugin, the soul skill's own STATE CHECK section detects the unpopulated state and pulls this same onboarding file. So you can EITHER:
1. Read `skills/soul/references/onboarding.md` directly and run it (when working from the cloned repo), OR
2. Let the soul skill's STATE CHECK auto-trigger it (when the user has plugin-installed and just invokes the skill).

Either path leads to the same flow. Source of truth is the `references/onboarding.md` file.

## Manual path (escape hatch)

If the user explicitly says they want to fill in templates manually, install the templates instead of running the SOUL onboarding:

```bash
cp -r skills/voice-hat-template ~/.claude/skills/
cp -r skills/platform-hat-template ~/.claude/skills/
```

Then tell them: open each `SKILL.md`, replace every `<<PLACEHOLDER>>`, rename the folder, and delete the "ESCAPE HATCH" callout. No further help unless they ask.

## After SOUL is installed: offer to derive a platform hat

Once SOUL is populated and installed, immediately offer the next high-value step:

> "Your SOUL is set up. If you write on specific platforms (LinkedIn, Reddit, Slack, etc.) and want a hat tuned to each, I can derive one now using the `platform-hat-deriver` skill. One platform at a time. Want to do that?"

If the user says yes:

1. Install `platform-hat-deriver` first if it is not already installed:
   ```bash
   cp -r skills/platform-hat-deriver ~/.claude/skills/
   ```
2. Then invoke the deriver's workflow inline (the full instructions live in `skills/platform-hat-deriver/SKILL.md`). It will:
   - Verify SOUL is populated.
   - Ask the user which platform.
   - Ask 4 to 6 platform-specific questions.
   - Draft a `<platform>-hat/SKILL.md`.
   - Show the draft for review.
   - Install on approval.
3. After the first hat is installed and validated, ask if the user wants another platform. ONE AT A TIME, never batch.

If the user declines, skip and continue to the "After install" section below.

## After install

Tell the user:

1. Installed skills live at `~/.claude/skills/<skill-name>/SKILL.md`.
2. The `description:` field in the frontmatter is what auto-triggers the skill. Customise it if needed.
3. They can invoke any skill manually with the `Skill` tool or `/<skill-name>` (depending on Claude Code version).
4. For `soul`: the more they iterate on the file over time, the better it gets. Add new examples whenever a particular phrasing feels right or wrong.
5. For derived platform hats: re-run `platform-hat-deriver` any time they want a new one. Each hat is a delta on SOUL, so SOUL updates propagate automatically.

## Do not

- Do not push or commit anything back to this repo without explicit user permission.
- Do not run SOUL onboarding without asking the user which mode they want.
- Do not paste user samples into anywhere except their Claude Code session.
- Do not batch-generate platform hats. One platform at a time so the user can validate each. The deriver supports this; do not bypass it.
- Do not assume the user wants all skills installed. Confirm first.

## If something goes wrong

- If `~/.claude/skills/` does not exist, create with `mkdir -p`.
- If a skill folder already exists at the destination, ask the user before overwriting.
- If sample mode would expose sensitive content, suggest the user redact or switch to interview mode.
