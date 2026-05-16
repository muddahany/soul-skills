# CLAUDE.md

> **For Claude Code:** This is an onboarding instructions file. The user has pointed you at this repo because they want to install one or more of these skills into their own Claude Code configuration. Follow the steps below.

## What this repo contains

A collection of Claude Code skills and templates. Three artifacts live in `skills/`:

| Skill | Type | What it does |
|---|---|---|
| `deslop` | Concrete skill, install as-is | Universal pass for catching AI-generated tells in any text draft (vocabulary, rhythm, tone). Platform-agnostic. |
| `voice-hat-template` | Template, requires customisation | Skeleton for encoding the user's personal writing voice into a skill. Has `<<PLACEHOLDER>>` markers. |
| `platform-hat-template` | Template, requires customisation | Skeleton for platform-specific writing rules (LinkedIn, Reddit, Slack, etc.). Has `<<PLACEHOLDER>>` markers. |

## Your job when the user lands here

1. **Greet the user briefly.** Tell them what this repo offers and ask which skills they want installed. Default offer: all three.
2. **Install the chosen skills.** Copy the relevant directories into the user's local skills folder.
3. **If they picked a template, offer to walk them through filling it in.** Ask the questions in the "Customisation prompts" section below. Do not force this; some users want to edit later.
4. **Verify the install and tell them what to do next** (restart Claude Code or use the Skill tool to invoke).

## Standard install location

- **macOS / Linux:** `~/.claude/skills/`
- **Windows:** `%USERPROFILE%\.claude\skills\`

Use the user's home directory. Do not install to a project-local directory unless the user explicitly asks for that.

## Install commands (macOS / Linux)

If running from inside this cloned repo:

```bash
mkdir -p ~/.claude/skills

# Install all three
cp -r skills/deslop ~/.claude/skills/
cp -r skills/voice-hat-template ~/.claude/skills/
cp -r skills/platform-hat-template ~/.claude/skills/
```

If the user does not have this repo cloned locally, clone it first:

```bash
git clone https://github.com/muddahany/claude-code-skills.git /tmp/claude-code-skills
cd /tmp/claude-code-skills
```

Then run the install commands above.

To install only one skill, copy that specific folder.

## Customisation prompts (templates only)

When the user wants to fill in `voice-hat-template`:

1. Ask: "Which 3-5 phrases do you NEVER want to see in your own writing?" (e.g., "leverage", "I hope this helps", "as a [role]")
2. Ask: "Any punctuation you want banned?" (em dashes are the common one)
3. Ask: "Describe how you sound in writing in one paragraph. Direct? Casual? Sarcastic? Specific?"
4. Ask: "Any positive style rules? (CAPS for emphasis, short paragraphs, lead with results, etc.)"
5. Open `~/.claude/skills/voice-hat-template/SKILL.md`. Replace every `<<PLACEHOLDER>>` with the user's answers.
6. Rename the folder to something personal (e.g., `mohamed-voice-hat`, or just `voice-hat` if they prefer).
7. Update the `name:` field in the frontmatter to match the folder name.
8. Update the `description:` field with specific triggers ("Use when drafting anything in [user's name]'s voice...").
9. Delete the "READ THIS FIRST" callout from the file.

When the user wants to fill in `platform-hat-template`:

1. Ask which platform (LinkedIn, Reddit, Slack, Discord, Twitter/X, Upwork, etc.).
2. Ask: "What makes a post on that platform look obviously AI-generated to you?"
3. Ask the platform's length norms ("how long is a typical good post or comment there?").
4. Ask about format constraints the platform rewards or punishes (headers, bullet lists, hashtags, emojis).
5. Open `~/.claude/skills/platform-hat-template/SKILL.md`. Replace every `<<PLACEHOLDER>>` with the user's answers.
6. Rename the folder to `<platform>-hat` (e.g., `linkedin-hat`, `reddit-hat`).
7. Update the `name:` and `description:` fields accordingly.
8. Delete the "READ THIS FIRST" callout.

## After install

Tell the user:

1. Skills are installed at `~/.claude/skills/<skill-name>/SKILL.md`.
2. The `description:` in the frontmatter is what auto-triggers the skill, so it loads when relevant requests come in.
3. They can manually invoke any skill with the `Skill` tool or by typing `/<skill-name>` (depending on their Claude Code version).
4. Templates require the placeholders to be filled in before they are useful. Show them the file path and either help them fill it in now or leave a TODO.

## Do not

- Do not push or commit anything back to this repo without explicit user permission.
- Do not install ATG-specific, org-specific, or any personal voice skills from this repo. This repo only contains the universal `deslop` skill and two voice-agnostic templates.
- Do not assume the user wants all three skills. Ask first.
- Do not skip the customisation step for templates. An uncustomised template is not useful.

## If something goes wrong

- If `~/.claude/skills/` does not exist, create it with `mkdir -p`.
- If a skill folder already exists at the destination, ask the user before overwriting.
- If you cannot reach GitHub (no network), tell the user to clone manually and re-invoke you with the local path.
