---
name: voice-hat-template
description: TEMPLATE skill. Copy this folder, rename it to YOUR-voice-hat (or similar), then fill in the placeholders below to encode YOUR personal writing voice. Triggers when drafting anything in your own voice. Replace this description with the specific triggers for your version.
---

# Voice Hat Template

> **ESCAPE HATCH FOR POWER USERS.** The recommended path is `soul` (interactive populate via the repo's onboarding flow), not this template. Use this file only if you want raw manual control over your voice rules or already know them by heart.
>
> Replace every `<<PLACEHOLDER>>` below with your own rules before using. Delete this callout when you do.

## Purpose

A voice hat enforces YOUR personal writing rules whenever Claude drafts text in your voice. Without one, Claude defaults to a corporate, hedged, em-dash-heavy register that does not sound like any real person. The hat makes sure the output sounds like YOU.

## When to Use

This skill should trigger any time you are writing AS YOURSELF in any external-facing context. Adjust the trigger list to match the platforms and use cases YOU write for. Examples:

- Drafting emails, DMs, or messages
- Writing social posts, comments, replies
- Producing proposals, cover letters, profile copy
- Any content where the "author voice" matters more than information density

## Voice Rules

Fill these in with YOUR rules. The categories below are the ones I found most useful after iterating; add or remove as needed.

### Banned characters and punctuation

List punctuation marks that you NEVER want in your output, with a one-line reason.

- `<<example: em dash (—). Use periods or commas instead. Reason: signals AI authorship.>>`
- `<<example: ellipsis (…). Use three periods. Reason: visual inconsistency.>>`
- `<<add your own>>`

### Banned phrases

Phrases that should never appear. These are the ones that make you cringe when you read your own work.

- `<<example: "excited to share">>`
- `<<example: "I hope this helps">>`
- `<<example: "as a [role]">>`
- `<<example: "leverage">>`
- `<<add your own>>`

### Required style rules

Positive rules. What MUST be true of the output.

- `<<example: results first, context after. Lead with the outcome, then explain.>>`
- `<<example: short paragraphs. 1 to 3 sentences each. No walls of text.>>`
- `<<example: CAPS for emphasis, not bold or italics.>>`
- `<<example: normal apostrophes in contractions (don't, isn't, won't).>>`
- `<<example: real numbers only. If you don't have them, don't invent them.>>`
- `<<add your own>>`

### Tone

One paragraph describing how you sound in writing. This is the texture rule that catches everything else.

> `<<example: Direct, conversational, a bit raw. Engineer talking to another engineer. No corporate hedging. No press-release voice. No assistant phrasing. Skeptical by default. Specific by default.>>`

## Workflow

1. **Read the draft fully** before flagging anything.
2. **Apply the rules in order:**
   - Banned characters: search-and-remove.
   - Banned phrases: search-and-rewrite.
   - Required style: check against each rule.
   - Tone: read aloud, ask "does this sound like me?"
3. **Rewrite specific lines** rather than the whole draft, unless tone violations are pervasive.
4. **Present the revised version** with a short diff summary explaining what changed.
5. **Wait for approval.** Voice is personal. Do not assume.

## Output Format

```
## Voice check

Banned characters found: [list with line numbers]
Banned phrases found: [list with line numbers]
Style violations: [list]
Tone verdict: [matches / drifts toward AI / drifts toward formal]

## Revised draft

[full revised text]

## What changed
- [bullet describing each change]
```

## Examples (replace with your own)

Before:
> `<<example: "I'm excited to share that we've leveraged our extensive experience to deliver a robust solution that helps clients navigate their cloud journey.">>`

After:
> `<<example: "We shipped this. Clients use it daily. Cut their AWS bill 40%.">>>`

## How to Use This Template

1. Copy this folder to `~/.claude/skills/your-name-voice-hat/`
2. Rename `voice-hat-template` to your skill name in the frontmatter `name:` field
3. Rewrite the `description:` field with specific triggers ("Use when drafting as [your name]...")
4. Replace every `<<PLACEHOLDER>>` with your actual rules
5. Delete the "READ THIS FIRST" callout
6. Test it by asking Claude to draft something and checking that the rules apply

## Tips

- Start with 3-5 banned phrases. Add more as you notice patterns in your own writing.
- The "Tone" paragraph is the catchall. Make it specific and grounded in real adjectives you would use to describe yourself.
- If you write in multiple registers (e.g., Slack vs. blog posts), make multiple hats and layer them with a platform-hat (see `platform-hat-template`).
- Re-read your own old writing for inspiration. Your real voice is already on the page, you just need to extract the rules.
