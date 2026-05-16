# CLAUDE.md

> **For Claude Code:** This is an onboarding instructions file. The user has pointed you at this repo because they want to install one or more skills into their own Claude Code configuration. Follow the steps below. Read the file fully before acting.

## What this repo contains

| Path | Type | Role |
|---|---|---|
| `skills/deslop/` | Universal skill | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/soul/` | Personalized skill, populated via onboarding | Encodes the user's personal voice, writing style, and values that shape voice. Drives all "write as me" use cases. **Recommended core skill.** |
| `skills/platform-hat-deriver/` | Meta-skill | Auto-generates platform-specific hats (LinkedIn, Reddit, Slack, etc.) from a populated SOUL plus a platform name. Run once per platform. |
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

1. **Plugin marketplace** (cleanest if Claude Code supports it for the user). Tell the user they can run `/plugin marketplace add muddahany/claude-code-skills` then `/plugin install deslop@muddahany-skills` (and similarly for `voice-hat-template`, `platform-hat-template`). Only use this for the non-SOUL skills, because SOUL needs the interactive onboarding flow below.
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

`soul` is the user's personal voice skill. It encodes how THEY sound on paper. The template lives at `skills/soul/SKILL.md` but it ships UNPOPULATED. Your job is to populate it through an interactive flow with the user.

### Step 2a: ask which mode the user wants

Present these three options clearly. Include a transparency note that anything they share goes through their Claude Code session.

1. **Sample mode** — user pastes 5 to 10 examples of their actual writing (past posts, emails, comments, messages). You extract patterns. Highest fidelity but requires them to dig up samples.
2. **Interview mode** — you ask 10 to 15 questions about how they write, what they hate seeing in their own work, what they want their voice to feel like. Slowest but no samples needed.
3. **Hybrid** — sample first, interview to fill gaps. Recommended for serious use.

Let the user pick. Do not default to one.

### Step 2b: run the chosen mode

**If SAMPLE mode:**

1. **Explicitly ask: are these samples GENUINELY YOUR writing, not AI-generated or heavily AI-edited?** If the user is unsure or admits the samples are AI-touched, switch to INTERVIEW mode. AI samples will pollute the soul.
2. Ask the user to paste 5 to 10 examples of writing that genuinely sounds like them. Variety helps: a blog post, a Slack message, a cold email, a Reddit comment.
3. Read through every sample. Extract patterns in these categories:
   - Banned characters (e.g., no em dashes, no ellipses)
   - Banned phrases (clichés, filler, AI-tells they avoid)
   - Required style rules (CAPS for emphasis, lead-with-result, short paragraphs, etc.)
   - Tone (one paragraph of texture)
   - Values that show up across samples (precision, skepticism, anti-corporate, etc.)
4. Note your CONFIDENCE on each extracted rule. Tag uncertain ones `[verify with user]` in the draft SOUL.md.

**If INTERVIEW mode:**

**Before starting**, recommend that the user answer by SPEAKING rather than typing, using voice-to-text (Wispr Flow, macOS Dictation, Whisper, or anything similar). Spoken answers expose authentic phrasing and natural rhythm that typed answers smooth over. This is the highest-leverage tip you can give them for this mode.

Ask these in order, one or two at a time. Adapt based on answers. Do not dump all 15 at once. If an answer feels short or AI-shaped, ask a followup ("can you say more about that?", "what's a specific example?") to draw out the real voice.

1. "How would you describe how you sound in writing in one sentence? A friend describing you."
2. "Which 3-5 phrases do you NEVER want to see in your own writing?"
3. "Any punctuation you want banned?" (em dash is the common one)
4. "Do you use CAPS for emphasis? Bold? Italics? Or none?"
5. "Short paragraphs or long ones?"
6. "Do you lead with the result or build up to it?"
7. "Do you hedge ('might', 'could', 'perhaps') or state directly?"
8. "How casual or formal? Slang OK? Curse words OK?"
9. "Do you use lists/bullets a lot or mostly flowing prose?"
10. "What's an example of writing you've seen that made you cringe? What was wrong with it?"
11. "What's an example of writing you've seen that made you nod? What was right about it?"
12. "Are there 2-3 values you hold that change how you write? (e.g., precision over politeness, numbers when you have them, skepticism by default)"
13. "Anything platform-specific that matters now? (e.g., you write a lot of Reddit comments, or LinkedIn posts)"

**If HYBRID:**

Run SAMPLE first. Then use INTERVIEW to fill gaps where the samples did not give you enough signal. Skip questions the samples answered.

### Step 2c: draft the populated SOUL.md

Take the user's `skills/soul/SKILL.md` (the template) and fill in every section with what you learned. Specifically:

- **Identity paragraph**: one paragraph in the user's voice about who they are AS A WRITER. Not job title.
- **Banned characters**: bullet list with brief reasons.
- **Banned phrases**: their actual list.
- **Required style rules**: positive rules they care about.
- **Writing style paragraph**: 1 to 2 paragraphs of tone description.
- **Values that shape voice**: 3 to 7 values. Only ones that actually change how they write.
- **Examples**: at least 2 before/after pairs. If they gave samples, use real ones (paraphrased if sensitive). If they did not, generate plausible ones and ask them to confirm.

Mark any rule you are uncertain about with `[verify]` so the user can spot-check on review.

Remove the "NOT YET POPULATED" callout at the top.

### Step 2d: show the draft to the user

Display the full populated SOUL.md. Ask:
- "Does this sound like you?"
- "Anything missing?"
- "Anything wrong?"

Iterate until the user is happy. Be willing to rewrite sections that miss.

### Step 2e: install

Write the final SOUL.md to `~/.claude/skills/soul/SKILL.md`:

```bash
mkdir -p ~/.claude/skills/soul
cp skills/soul/SKILL.md ~/.claude/skills/soul/SKILL.md
# then overwrite with the populated version you just drafted
```

In practice, since you have edited the version in the repo working tree during onboarding, the cleanest sequence is: edit the repo's `skills/soul/SKILL.md` in place during drafting, then `cp -r skills/soul ~/.claude/skills/` once approved. Make sure the repo's original template is restored or noted as "user's working copy" so the user is not confused.

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
