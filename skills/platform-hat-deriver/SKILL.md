---
name: platform-hat-deriver
description: Use to AUTOMATICALLY generate a platform-specific writing hat from the user's populated SOUL primitive plus a platform name. Trigger on requests like "create a LinkedIn hat", "make me a Reddit hat", "derive a platform hat for Slack", "build a Twitter writing skill", "I need a Discord hat", "generate a platform-specific voice for [X]". Built-in reference covers LinkedIn, Reddit, Slack, Twitter/X, Discord, GitHub, Substack, and email syntax (public facts, no user input needed). Only the personal/contextual rules (failure modes per the user's audience, tone overlay, samples) are asked. REQUIRES SOUL to be populated first; if not, point the user at the SOUL onboarding in soul-skills/CLAUDE.md. One run produces one hat. Run the skill again for additional platforms. This is the recommended path over the manual platform-hat-template.
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
4. If any check fails, STOP. Tell the user: "Your SOUL is not populated yet. Run the SOUL onboarding first (see soul-skills/CLAUDE.md) before deriving platform hats. A platform hat derived from an empty SOUL would inherit garbage."
5. Do not proceed until SOUL is verified populated.

## Workflow

### Step 1: Confirm the platform

Ask: "Which platform is this hat for? (LinkedIn, Reddit, Slack, Discord, Twitter/X, Upwork, GitHub, email, Substack, etc.)"

Lower-case and kebab-case the answer. Use it as the skill folder name: `<platform>-hat`. Examples:
- "LinkedIn" → `linkedin-hat`
- "Twitter/X" → `twitter-hat`
- "Upwork" → `upwork-hat`

If the user already has a hat at `~/.claude/skills/<platform>-hat/`, ask whether to overwrite, pick a new name, or cancel.

### Step 2: Resolve platform syntax (from known reference, not from the user)

Platform syntax is public, factual, and stable. Look it up in the "Known platforms" reference section below. Do NOT ask the user. If the platform is listed, pre-fill the Syntax section of the generated hat from the reference. Show it to the user briefly with one prompt: "Here is what I know about [platform]'s syntax. Anything wrong or outdated?" Move on quickly unless they correct something.

If the platform is NOT in the reference (niche forum, internal company tool, new platform), THEN ask the syntax questions:
- Does it render full markdown, a variant, or no markdown?
- Bold syntax (`**bold**` / `*bold*` / not supported)?
- Italics syntax?
- Headers allowed where?
- Code blocks?
- Inline links?
- Mentions syntax?
- Hashtags?
- Line break behaviour?
- Character limit?

### Step 3: Gather personal and contextual rules (from the user, always)

These cannot be looked up. Ask 9 questions, one or two at a time. Recommend voice-to-text (Wispr Flow, macOS Dictation, Whisper) for richer answers.

1. **Failure modes:** "What makes a post on [platform] look obviously AI-generated to YOU? Give 2 to 3 specific tells you have noticed."
2. **Tone overlay:** "How does YOUR voice adjust for this platform versus how you write elsewhere? More casual, more formal, more direct, more performative?"
3. **Target channels / audience:** "WHERE on [platform] will you post? Specific subreddits, channels, audiences, lists, or contact segments? For each, what kind of contribution do you bring?"
4. **Hard limits:** "What are 3 to 5 things you will NEVER do on this platform? Hard limits, not preferences."
5. **Post structure:** "What is the optimal structure for a post or message on this platform? (e.g., for LinkedIn: Hook → Context → Turn → Takeaway → Close; for Reddit comments: one point → support → stop; for Slack: ask + one-line context; for cold email: relevance → insight → ask). Describe the skeleton."
6. **Hook formulas (if applicable):** "Are there specific opening formulas that work on this platform? (e.g., specific number, confession, counterintuitive, story entry, direct challenge). Give 3 to 5 you have seen work."
7. **Samples:** "Do you have 2 to 3 real examples of posts on this platform that match the register you want? Paste them. Samples beat descriptions." (optional but high-value)
8. **AI detection signals:** "Beyond generic AI tells, are there platform-specific signals that get a post flagged as AI by THIS community? 3 to 6 checklist items."
9. **Community quirks:** "Anything else community-specific that matters? Algorithm behaviour, audience expectations, community taboos, posting cadence."

If the user gives weak or AI-shaped answers, ask followups ("can you say more about that?", "what's a specific example?"). Do NOT fabricate.

### Step 4: Synthesize the deltas

Combine the looked-up syntax (Step 2) with the personal/contextual rules (Step 3):

- **Platform syntax** (Step 2): from the reference, or from the user if unknown.
- **Target channels and audience** (Step 3 q3): where the user posts, what they bring to each.
- **Length norms**: from the reference where available, refined by the user's typical-good-post answer.
- **Tone overlay** (Step 3 q2): 1 to 2 paragraphs on register adjustment.
- **Post structure** (Step 3 q5): the skeleton for a post or message. Numbered steps.
- **Hook formulas** (Step 3 q6 — for platforms with feeds/posts): 3 to 5 opening patterns the user has seen work.
- **Hard limits** (Step 3 q4): non-negotiable "never do this" rules.
- **Failure modes** (Step 3 q1): platform-specific AI-tells.
- **AI detection checklist** (Step 3 q8): platform-specific signals that get flagged as AI. Convert each tell into a `[ ]` checkbox item.
- **Required structural rules** (Step 3 q9): community/algorithm quirks.

Anything uncertain, tag `[verify]` in the draft.

### Step 5: Draft the hat

Generate a SKILL.md at `~/.claude/skills/<platform>-hat/SKILL.md` using this structure:

```markdown
---
name: <platform>-hat
description: Use when drafting content for <Platform>. Trigger on requests like "write a <platform> post", "draft this for <platform>", "<platform> reply", or when the user explicitly mentions <platform>. Layered on top of `soul`: SOUL provides the base voice; this hat applies <platform>-specific syntax, format, length, tone overlay, failure-mode checks, hard limits, and AI-detection check. Final step copies the output to clipboard.
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

## Target channels and audience

Where on this platform the user will post and what they bring to each.

[From Step 3 question 3. Examples:
- **r/aws** — cost optimization war stories and specific dollar wins
- **r/devops** — real incident lessons, no theory
- **DevOps Slack #infra-chat** — quick wins, code snippets only
- ...]

## Length norms

[Specific guidance with numbers, e.g., "Posts: 150-300 words. Replies: under 100."]

## Tone overlay

[1 to 2 paragraphs describing how the user's voice adjusts for this platform]

## Post / message structure

[The skeleton the user follows. Numbered steps. Examples:
- For LinkedIn posts: 1) Hook (2 lines max) 2) Context 3) Turn / insight 4) Takeaway (one, not three) 5) Close
- For Reddit comments: 1) Answer in the first sentence 2) Support if needed 3) Stop
- For cold email: 1) Relevance sentence 2) One insight 3) One ask
Use the user's actual structure.]

## Hook formulas (if applicable)

[3 to 5 opening patterns the user has seen work on this platform. Examples for LinkedIn:
- Specific number: "We cut $14K/mo from one Lambda function."
- Confession: "I deleted 200 alarms last week."
- Counterintuitive: "The most expensive service isn't the one you monitor."
- Story entry: "A client called at 11pm because the bill doubled."
- Direct challenge: "Most microservices architectures are distributed monoliths."
Skip if the platform has no concept of feed-style posts (e.g., Slack, email).]

## Hard limits (never do these)

The user's explicit no-go rules for this platform. Non-negotiable.

[From Step 3 question 4. Examples:
- Never link to own site unprompted
- Never mention client names
- Never start a comment with "As a [role]"
- Never use hashtags
- ...]

## Failure modes specific to <Platform>

[Bulleted list of platform-specific AI-tells. These get an automatic rewrite.]

## AI detection checklist (run before publishing)

Platform-specific signals that this community flags as AI. Run this checklist on EVERY draft before clipboard copy.

[From Step 3 question 6. Examples for Reddit:
- [ ] No em dashes anywhere
- [ ] No "It's worth noting that..." or "That said,..."
- [ ] No headers or bullets in comments
- [ ] No "I'd recommend..." (say "Try..." or "Use...")
- [ ] No three-adjective triads ("robust, seamless, and innovative")
- ...]

## Required structural rules (if any)

[Things the algorithm or community explicitly rewards]

## Workflow

1. Apply soul rules first.
2. Apply tone overlay (register adjustment).
3. Apply format constraints AND platform syntax. Convert markdown to the variant the platform actually renders. Strip what is unsupported.
4. Run failure-mode check; rewrite any matches.
5. Run the AI detection checklist. EVERY item must pass before proceeding.
6. Verify against Hard Limits. Any hit = stop and rewrite that section.
7. Trim or expand to length norms. Enforce character limit if any.
8. Present the revised draft with a short summary of what changed, including which AI-detection items were caught and rewritten.
9. Wait for user approval.
10. **Copy the approved draft to the clipboard.** Use `pbcopy` on macOS, `xclip -selection clipboard` on Linux, or `clip.exe` on Windows. Use HEREDOC or `printf '%s'` for multi-line content so newlines are preserved. Confirm to the user: "Copied to clipboard."

## Examples (where available)

[Before/after pairs from user samples if provided, else generated examples flagged for user verification]
```

### Step 6: Show the draft to the user

Display the full generated SKILL.md. Ask:

- "Does this match how you actually write on [platform]?"
- "Anything missing or wrong?"
- "Are the format constraints accurate?"
- "Is the failure-mode list complete, or are there other tells I missed?"

Iterate. Be willing to rewrite sections. Voice-to-text helps users articulate refinements quickly.

### Step 7: Install

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

---

## Known platforms reference

Use this section to look up platform syntax in Step 2. These conventions are public, factual, and reasonably stable. Last updated 2026-05. If a user reports something here is wrong or outdated, trust their correction and update this file.

### LinkedIn

- **Markdown:** NO (post body renders as plain text)
- **Bold:** not supported (Unicode workarounds discouraged, look performative)
- **Italics:** not supported
- **Headers:** not supported
- **Code blocks:** not supported
- **Inline links:** autolinks only (paste URL, will be clickable)
- **Mentions:** `@user` with tag completion in the composer
- **Hashtags:** clickable, limit 3 per post is the common-wisdom max
- **Line breaks:** single newline respected, blank line for paragraph break
- **Character limits:** posts 3,000; comments 1,250; headlines 220; about section 2,600

### Reddit

- **Markdown:** subset, Reddit's own flavor (Fancy Pants Editor)
- **Bold:** `**bold**`
- **Italics:** `*italic*` or `_italic_`
- **Strikethrough:** `~~strike~~`
- **Headers:** `# header` allowed in posts, NOT in comments
- **Code blocks:** triple backticks fenced; indent 4 spaces for legacy
- **Inline links:** `[text](url)`
- **Mentions:** `u/username` (no @ symbol)
- **Hashtags:** NOT clickable, do not work
- **Line breaks:** blank line = paragraph break; single newline is collapsed unless you double-space at end of line
- **Subreddit links:** `r/subname`
- **Character limits:** posts 40,000; comments 10,000; titles 300

### Slack

- **Markdown:** mrkdwn variant (Slack's own, NOT standard markdown)
- **Bold:** `*bold*` (SINGLE asterisks, not double; this is the most common mistake)
- **Italics:** `_italic_`
- **Strikethrough:** `~strike~` (single tilde, not double)
- **Headers:** not supported
- **Code blocks:** triple backticks fenced; single backticks inline
- **Inline links:** `<url|text>` (NOT standard markdown syntax)
- **Mentions:** `<@USERID>` programmatically; `@user` in the composer
- **Hashtags:** NOT clickable; channel links use `<#CHANNELID|name>` or `#channel` in composer
- **Line breaks:** respected as written (shift+enter for newline within message)
- **Character limit:** ~4,000 soft per message; ~40,000 hard

### Twitter / X

- **Markdown:** NONE
- **Bold:** not supported (Unicode workarounds frowned on)
- **Italics:** not supported
- **Headers:** not supported
- **Code blocks:** not supported
- **Inline links:** autolinks only; URLs count as 23 chars regardless of length
- **Mentions:** `@user`
- **Hashtags:** clickable, common wisdom: max 2 per tweet
- **Line breaks:** respected as written
- **Character limit:** 280 free tier, 25,000 Premium

### Discord

- **Markdown:** yes, full
- **Bold:** `**bold**`
- **Italics:** `*italic*` or `_italic_`
- **Strikethrough:** `~~strike~~`
- **Underline:** `__underline__`
- **Spoiler:** `||spoiler||`
- **Headers:** `# H1`, `## H2`, `### H3` (3 levels only)
- **Code blocks:** triple backticks with optional language for syntax highlighting; single backticks inline
- **Inline links:** `[text](url)` works in some channels (embeds), autolinks elsewhere
- **Mentions:** `<@USERID>` programmatically; `@user` in composer
- **Hashtags:** NOT clickable in messages (only used for channel routing)
- **Line breaks:** respected (shift+enter for newline within message)
- **Character limit:** 2,000 per message; 4,000 with Nitro

### GitHub (Issues, PRs, comments, README)

- **Markdown:** full GFM (GitHub Flavored Markdown)
- **Bold:** `**bold**`
- **Italics:** `*italic*` or `_italic_`
- **Strikethrough:** `~~strike~~`
- **Headers:** `# H1` through `###### H6`
- **Code blocks:** triple backticks with language tag for syntax highlighting
- **Inline links:** `[text](url)`
- **Mentions:** `@user` or `@org/team`
- **References:** `#123` for issues/PRs in same repo, `owner/repo#123` cross-repo
- **Hashtags:** not a concept
- **Line breaks:** GFM is more lenient than standard MD; single newline often treated as line break in lists and tables
- **Character limit:** 65,536 per comment

### Substack

- **Markdown:** yes, in their editor
- **Bold:** `**bold**`
- **Italics:** `*italic*` or `_italic_`
- **Headers:** yes, H1-H4
- **Code blocks:** triple backticks
- **Inline links:** `[text](url)`
- **Mentions:** `@author` for cross-Substack mentions
- **Hashtags:** not used
- **Character limit:** none in practice; long-form expected

### Email (plain text, safest default)

- **Markdown:** depends on client; assume NO unless writing to a known-rich-text client
- **Bold/italics:** plain text uses convention `*emphasis*` or `_emphasis_` but not rendered
- **Headers:** text-based only (UPPERCASE or hyphen-underline)
- **Code blocks:** indent or use line breaks
- **Inline links:** paste full URL
- **Mentions:** not a concept
- **Line breaks:** preserve exactly as written; many clients soft-wrap
- **Character limits:** no hard cap; SMTP body practical limit much higher than you would write

### Adding a new platform to this reference

Open a PR. Include the same 10 fields. Cite a source if the data is non-obvious. Date the addition.
