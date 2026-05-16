# CLAUDE.md

> **For Claude Code:** This is an onboarding instructions file. The user has pointed you at this repo because they want to install one or more skills into their own Claude Code configuration. Follow the steps below. Read the file fully before acting.

## What this repo contains

| Path | Type | Role |
|---|---|---|
| `skills/deslop/` | Universal skill | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/soul/` | Personalized skill, populated via onboarding | Encodes the user's personal voice, writing style, and values that shape voice. Drives all "write as me" use cases. **Recommended core skill.** |
| `skills/voice-hat-template/` | Manual template, escape hatch | Raw skeleton with placeholders. Only for users who want manual control instead of the SOUL onboarding. |
| `skills/platform-hat-template/` | Manual template, escape hatch | Raw skeleton for platform-specific writing rules. Future: a deriver skill will auto-generate these from SOUL + platform name. |

## Your job when the user lands here

1. **Greet the user briefly** and tell them what is available. Suggest the recommended path: install `deslop` + populate `soul`. Mention the manual template path exists if they ask.
2. **Confirm their choice.** Default offer: `deslop` + interactive `soul` setup.
3. **Install `deslop`** with a straight `cp -r`. No customisation needed.
4. **Populate `soul`** using the onboarding flow below. This is the high-leverage step.
5. **Verify everything is in place** and tell them what to do next.

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

1. Ask the user to paste 5 to 10 examples of writing that genuinely sounds like them. Variety helps: a blog post, a Slack message, a cold email, a Reddit comment.
2. Read through every sample. Extract patterns in these categories:
   - Banned characters (e.g., no em dashes, no ellipses)
   - Banned phrases (clichés, filler, AI-tells they avoid)
   - Required style rules (CAPS for emphasis, lead-with-result, short paragraphs, etc.)
   - Tone (one paragraph of texture)
   - Values that show up across samples (precision, skepticism, anti-corporate, etc.)
3. Note your CONFIDENCE on each extracted rule. Tag uncertain ones `[verify with user]` in the draft SOUL.md.

**If INTERVIEW mode:**

Ask these in order, one or two at a time. Adapt based on answers. Do not dump all 15 at once.

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

## After install

Tell the user:

1. Installed skills live at `~/.claude/skills/<skill-name>/SKILL.md`.
2. The `description:` field in the frontmatter is what auto-triggers the skill. Customise it if needed.
3. They can invoke any skill manually with the `Skill` tool or `/<skill-name>` (depending on Claude Code version).
4. For `soul`: the more they iterate on the file over time, the better it gets. Add new examples whenever a particular phrasing feels right or wrong.

## Do not

- Do not push or commit anything back to this repo without explicit user permission.
- Do not run SOUL onboarding without asking the user which mode they want.
- Do not paste user samples into anywhere except their Claude Code session.
- Do not auto-generate platform hats during onboarding. The deriver is V2.
- Do not assume the user wants all skills installed. Confirm first.

## If something goes wrong

- If `~/.claude/skills/` does not exist, create with `mkdir -p`.
- If a skill folder already exists at the destination, ask the user before overwriting.
- If sample mode would expose sensitive content, suggest the user redact or switch to interview mode.
