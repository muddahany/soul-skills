---
name: platform-hat-deriver
description: Use to AUTOMATICALLY generate a platform-specific writing hat from the user's populated SOUL primitive plus a platform name. Trigger on requests like "create a LinkedIn hat", "make me a Reddit hat", "derive a platform hat for Slack", "build a Twitter writing skill", "I need a Discord hat", "generate a platform-specific voice for [X]". REQUIRES SOUL to be populated first; if not, point the user at the SOUL onboarding in claude-code-skills/CLAUDE.md. One run produces one hat. Run the skill again for additional platforms. This is the recommended path over the manual platform-hat-template for most users.
---

# Platform Hat Deriver

## Overview

A meta-skill that generates personalized platform-specific writing skills from the user's SOUL plus a platform name. One run = one new hat. Run it multiple times for multiple platforms (LinkedIn, Reddit, Slack, Discord, Twitter/X, Upwork, GitHub, email, etc.).

The output hat is a thin DELTA on top of SOUL: same underlying voice, platform-tuned register, format constraints, length norms, and failure modes. The hat references SOUL rather than copying its rules, so updates to SOUL propagate automatically.

## Prerequisites

Before doing anything else, verify SOUL exists and is populated.

1. Check `~/.claude/skills/soul/SKILL.md` exists.
2. Open the file. Confirm it does NOT contain the "NOT YET POPULATED" callout.
3. Confirm the Identity, Voice rules, Writing style, and Values sections have real content, not placeholders.
4. If any check fails, STOP. Tell the user: "Your SOUL is not populated yet. Run the SOUL onboarding first (see claude-code-skills/CLAUDE.md) before deriving platform hats. A platform hat derived from an empty SOUL would inherit garbage."
5. Do not proceed until SOUL is verified populated.

## Workflow

### Step 1: Confirm the platform

Ask: "Which platform is this hat for? (LinkedIn, Reddit, Slack, Discord, Twitter/X, Upwork, GitHub, email, Substack, etc.)"

Lower-case and kebab-case the answer. Use it as the skill folder name: `<platform>-hat`. Examples:
- "LinkedIn" → `linkedin-hat`
- "Twitter/X" → `twitter-hat`
- "Upwork" → `upwork-hat`

If the user already has a hat at `~/.claude/skills/<platform>-hat/`, ask whether to overwrite, pick a new name, or cancel.

### Step 2: Gather platform conventions

Ask 4 to 6 questions, one or two at a time. Adapt based on answers. Recommend voice-to-text (Wispr Flow, macOS Dictation, Whisper) for richer answers.

1. "What makes a post on [platform] look obviously AI-generated to you? Give 2 to 3 specific tells you have noticed."
2. "What is the typical length of a good post or comment there?" (word count or rough range)
3. **Platform syntax** (the most important question, ask explicitly). "What is the SYNTAX of this platform? Specifically:
   - Does it render full markdown, a markdown variant (Slack mrkdwn, Reddit's subset, etc.), or no markdown at all?
   - Bold syntax: `**bold**`, `*bold*`, `_bold_`, or none?
   - Italics syntax: `*italic*`, `_italic_`, or none?
   - Headers allowed? In posts, in comments, both, or never?
   - Code blocks: triple backticks, single backticks for inline, or unsupported?
   - Inline links: markdown `[text](url)`, auto-link only, numbered references, or none?
   - Mentions: `@user`, `u/user`, `<@user>`, or no mentions?
   - Hashtags: clickable, just text, or skip entirely?
   - Line breaks: single newline = paragraph, or do you need a blank line?
   - Character limit: any hard cap? (Twitter: 280, LinkedIn ~3000, etc.)"
4. "How does YOUR voice adjust for this platform versus how you write elsewhere? More casual, more formal, more direct, more performative?"
5. "Do you have 2 to 3 real examples of posts on this platform that match the register you want? Paste them if you do. Samples beat descriptions." (optional but high-value)
6. "Anything else specific to this platform that matters? Algorithm quirks, audience expectations, community taboos, posting cadence."

If the user gives weak or AI-shaped answers, ask followups ("can you say more about that?", "what's a specific example?"). Do NOT fabricate platform rules you do not have evidence for.

### Step 3: Extract the platform deltas

From the user's answers, identify and write down:

- **Platform syntax**: markdown variant, bold/italic syntax, headers, code blocks, links, mentions, hashtags, line-break behaviour, character limits. This is the most concrete section; encode it precisely so the hat can mechanically enforce it.
- **Format constraints**: what the platform UI rewards or punishes (length, structure, format).
- **Length norms**: numeric guidance for posts and replies.
- **Failure modes**: platform-specific tells that mark a post as AI-generated to that community.
- **Tone overlay**: a 1 to 2 paragraph description of how the user's voice adjusts for this platform's register.
- **Required structural rules**: anything the platform's algorithm or culture explicitly rewards or expects.

Anything you are uncertain about, tag `[verify]` in the draft so the user can spot-check.

### Step 4: Draft the hat

Generate a SKILL.md at `~/.claude/skills/<platform>-hat/SKILL.md` using this structure:

```markdown
---
name: <platform>-hat
description: Use when drafting content for <Platform>. Trigger on requests like "write a <platform> post", "draft this for <platform>", "<platform> reply", or when the user explicitly mentions <platform>. Layered on top of `soul`: SOUL provides the base voice; this hat applies <platform>-specific syntax, format, length, tone overlay, and failure-mode checks. Final step copies the output to clipboard.
---

# <Platform> Hat

> **Layered on top of `soul`.** Apply soul voice rules first (banned characters, banned phrases, required style, writing style, values). Then apply the <platform>-specific overrides below.

## Platform syntax

This is the rendering surface. The output MUST conform exactly or the post breaks.

- **Markdown support:** [full / variant / none] — [variant name if applicable]
- **Bold syntax:** [`**bold**` / `*bold*` / `_bold_` / not supported]
- **Italics syntax:** [`*italic*` / `_italic_` / not supported]
- **Headers:** [allowed in posts / allowed in comments / not at all]
- **Code blocks:** [triple backticks / inline only / not supported]
- **Inline links:** [markdown / autolink only / numbered references / not supported]
- **Mentions:** [`@user` / `u/user` / `<@user>` / not supported]
- **Hashtags:** [clickable / text only / skip]
- **Line breaks:** [single newline = paragraph / blank line required]
- **Character limit:** [hard cap if any, e.g., 280 for Twitter, ~3000 for LinkedIn, none otherwise]

## Format constraints

[Bulleted list extracted from user's answers]

## Length norms

[Specific guidance with numbers, e.g., "Posts: 150-300 words. Replies: under 100."]

## Tone overlay

[1 to 2 paragraphs describing how the user's voice adjusts for this platform]

## Failure modes specific to <Platform>

[Bulleted list of platform-specific AI-tells. These get an automatic rewrite.]

## Required structural rules (if any)

[Things the algorithm or community explicitly rewards]

## Workflow

1. Apply soul rules first.
2. Apply tone overlay (register adjustment).
3. Apply format constraints AND platform syntax. Convert markdown to the variant the platform actually renders. Strip what is unsupported.
4. Run failure-mode check; rewrite any matches.
5. Trim or expand to length norms. Enforce character limit if any.
6. Present the revised draft with a short summary of what changed.
7. Wait for user approval.
8. **Copy the approved draft to the clipboard.** Use `pbcopy` on macOS, `xclip -selection clipboard` on Linux, or `clip.exe` on Windows. Use HEREDOC or `printf '%s'` for multi-line content so newlines are preserved. Confirm to the user: "Copied to clipboard."

## Examples (where available)

[Before/after pairs from user samples if provided, else generated examples flagged for user verification]
```

### Step 5: Show the draft to the user

Display the full generated SKILL.md. Ask:

- "Does this match how you actually write on [platform]?"
- "Anything missing or wrong?"
- "Are the format constraints accurate?"
- "Is the failure-mode list complete, or are there other tells I missed?"

Iterate. Be willing to rewrite sections. Voice-to-text helps users articulate refinements quickly.

### Step 6: Install

Write the final SKILL.md to `~/.claude/skills/<platform>-hat/SKILL.md`. Confirm the file is in place. Tell the user:

- "The `<platform>-hat` skill is now installed at `~/.claude/skills/<platform>-hat/SKILL.md`."
- "It will trigger when you draft <Platform> content. SOUL will load first as the base voice."
- "If you want hats for other platforms, run the deriver again. One platform at a time so you can validate each."

## Anti-patterns

- Do not derive a hat if SOUL is not populated. The hat would inherit garbage. STOP and run SOUL onboarding first.
- Do not derive hats for multiple platforms in one batch. One at a time. Each needs user validation.
- Do not invent platform conventions you do not have evidence for. If the user gives weak answers and you cannot fill the gaps, ask followups, do not fabricate.
- Do not duplicate rules already in SOUL inside the hat. The hat is a DELTA, not a copy. References to SOUL are explicit.
- Do not make hats longer than ~120 lines. Brevity preserves user intent and keeps context cost low.
- Do not skip the prerequisite check. Empty SOUL = wasted hat.

## When to use

- User explicitly says "create a [platform] hat" or similar.
- User has just finished SOUL onboarding and asks for the next step.
- User mentions wanting to write differently on a specific platform.
- User says they get downvoted, ignored, or flagged as AI on a specific platform.

## When NOT to use

- SOUL is not populated yet. Run SOUL onboarding first.
- User wants a fully manual platform-hat with full control over every line. Direct them to `platform-hat-template`.
- User wants to modify an EXISTING hat. Edit the file directly rather than regenerating.
- User wants a generic universal-voice skill, not platform-specific. SOUL alone is enough.

## Tips

- The failure-mode list is the single highest-leverage section. Spend the most time there.
- If the user has 3+ real platform samples, sample-mode extraction is far better than question-only answers. Push for samples when possible.
- After deriving the hat, suggest the user test it once on a real draft and tweak based on output.
