---
name: platform-hat-template
description: MANUAL TEMPLATE only for platform-specific writing rules. Use when the user wants to manually encode the writing conventions of a specific platform (LinkedIn, Reddit, Slack, Discord, Twitter/X, Upwork, GitHub, etc.) without waiting for the V2 platform-hat-deriver that will auto-generate these from SOUL. Triggers on phrases like "create a LinkedIn hat", "platform-specific voice rules", "Reddit writing rules", "Slack tone overlay", "Twitter format hat". Once copied and renamed, the user must replace every <<PLACEHOLDER>> with platform-specific rules. Layered on top of a personal voice hat or SOUL.
---

# Platform Hat Template

> **ESCAPE HATCH FOR POWER USERS.** Once `soul` exists in your skills folder, a future version of this repo will offer a platform-hat-deriver skill that generates platform hats automatically from your SOUL plus a platform name. Use this template only if you want raw manual control or are building a hat before the deriver lands.
>
> Replace every `<<PLACEHOLDER>>` below with rules specific to the platform you are writing for. Delete this callout when you do.

> **Genuineness check.** Read the actual platform for at least an hour BEFORE filling this in. Note what real, well-received posts look like vs. obviously AI-generated ones. Your platform rules should come from what you observed, not what you imagine the platform wants. AI-imagined platform rules produce posts that get downvoted as slop.

## Purpose

A platform hat enforces the conventions of a specific platform on top of your personal voice. LinkedIn rewards different writing than Reddit, which rewards different writing than Slack DMs. A voice hat says "sound like me." A platform hat says "and follow this platform's rules."

Stack a platform hat ON TOP of a voice hat. Voice hat keeps you sounding like yourself; platform hat keeps the format and tone appropriate for where you are posting.

## When to Use

Trigger this skill when drafting content for a specific platform. Replace `PLATFORM` below with the actual one (LinkedIn, Reddit, Twitter/X, Slack, Discord, Upwork, GitHub, etc.).

- Drafting posts, replies, or DMs for `<<PLATFORM>>`
- Reformatting existing copy for a platform-specific channel
- When user mentions the platform name explicitly

## Platform Conventions

Fill these in with the rules specific to YOUR target platform. Categories below are starting points; adapt as needed.

### Format constraints

What does the platform's UI reward or punish?

- `<<example for Reddit: avoid headers, avoid heavy bolding, avoid bullet lists in short comments. Reddit's WYSIWYG rendering makes formatted content read as "trying too hard.">>`
- `<<example for LinkedIn: no hashtags above 3, no first-sentence hook clichés ("Here's why this matters"), no line-break ladders.>>`
- `<<example for Slack: no headers, no horizontal rules, code in triple backticks for >2 lines.>>`
- `<<add your own>>`

### Length norms

What does the platform's audience expect?

- `<<example for Reddit: comments under 200 words, posts under 500 unless the topic justifies it.>>`
- `<<example for LinkedIn: 150-300 words for posts. Under 100 for comments.>>`
- `<<example for Slack: 1-3 sentences for most messages. Thread for anything longer.>>`
- `<<add your own>>`

### Tone overlay

How does YOUR voice need to adjust for this platform?

- `<<example for Reddit: more casual than your default. Sentence fragments OK. Light typos OK (signals human).>>`
- `<<example for LinkedIn: more professional but NOT corporate. Specific over vague. No buzzwords.>>`
- `<<example for Upwork: focused on the client's problem, not your skills. Lead with their pain.>>`
- `<<add your own>>`

### Failure modes specific to this platform

What does the platform community immediately recognize as low-quality or AI-generated?

- `<<example for Reddit: opening with "TL;DR", numbered lists in casual posts, "Great question!" replies, em dashes.>>`
- `<<example for LinkedIn: humblebrag openers ("I'm humbled to share..."), three-word punchy lines stacked into a "ladder", crying-emoji-as-emphasis.>>`
- `<<example for Twitter/X: thread-baiting ("A thread:🧵"), promised "value bombs" that never arrive.>>`
- `<<add your own>>`

### Required structural rules

Anything the platform's algorithm or culture explicitly rewards.

- `<<example for Reddit: lowercase first word of comments is fine, even encouraged in some subreddits.>>`
- `<<example for LinkedIn: line break after every 1-2 sentences for readability in feed view.>>`
- `<<add your own>>`

## Workflow

1. **Confirm the platform context.** If unclear, ask.
2. **Apply the personal voice hat first** (if you have one). Voice rules are the base layer.
3. **Apply this platform's format constraints.** Strip or add what the platform expects.
4. **Apply the tone overlay.** Same voice, platform-adjusted register.
5. **Run the failure-mode check.** Catch the platform-specific cringe before publishing.
6. **Length check.** Cut to the platform's norm.

## Output Format

```
## Platform check (<<PLATFORM>>)

Format violations: [list]
Length: [current word/char count vs. platform norm]
Tone overlay: [appropriate / too formal / too casual]
Failure modes: [list any caught]

## Revised draft

[full revised text]

## What changed
- [bullet]
```

## Examples (replace with your own)

Before (for `<<PLATFORM>>`):
> `<<example: corporate-toned draft that violates platform conventions>>`

After (for `<<PLATFORM>>`):
> `<<example: platform-appropriate rewrite that still sounds like the author>>`

## How to Use This Template

1. Copy this folder to `~/.claude/skills/<<platform>>-hat/` (e.g., `linkedin-hat/`, `reddit-hat/`)
2. Rename `platform-hat-template` to your skill name in the frontmatter `name:` field
3. Rewrite the `description:` field with specific triggers for that platform
4. Replace every `<<PLACEHOLDER>>` with platform-specific rules
5. Delete the "READ THIS FIRST" callout
6. Test it by drafting platform-appropriate content and checking that conventions apply

## Tips

- Make ONE platform hat per platform. Do not try to make a generic "social media hat."
- The "Failure modes" section is the highest-leverage. These are the patterns that get a post flagged as low quality or AI-generated WITHIN seconds.
- Read the actual platform for an hour before writing the hat. Note what makes good posts good and bad posts obvious. Encode that.
- Update the hat when the platform's norms shift. LinkedIn 2024 != LinkedIn 2026.
