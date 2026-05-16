---
name: soul
description: Use whenever drafting any external-facing text in the user's personal voice. ALWAYS load when the user is composing emails, social posts, proposals, comments, profile bios, cover letters, replies, DMs, README files, or any author-attributed writing. ALSO trigger on setup requests like "set up my soul", "onboard soul", "configure soul", "populate soul", "soul setup", "/soul", "I just installed soul", "what now", or any time the user has just installed soul-skills and is unsure what to do next. Encodes the user's voice rules, writing style, perceptual filters, values, identity, current focus, and expression non-negotiables. Self-onboarding: if this file contains the "STATE CHECK" section below, the skill is unpopulated and Claude must run the onboarding in references/onboarding.md before applying voice rules.
user-invocable: true
---

# Soul

## STATE CHECK (do this FIRST when this skill loads)

**This skill is currently UNPOPULATED.** Before doing any voice work, you MUST run the interactive onboarding to fill in the user's voice.

**Action right now:**

1. Tell the user: "Your SOUL skill is not populated yet. Without that, I cannot apply your voice. Setting it up takes 20 to 40 minutes done well. Want to do it now?"
2. If yes: load `references/onboarding.md` from this skill's directory (`~/.claude/skills/soul/references/onboarding.md`) and run that flow end to end.
3. If no: tell them they can run `/soul` or say "set up my SOUL" later. Do not attempt voice work; just defer back to the user's original request without applying soul rules.

Once onboarding completes, the populated SOUL.md replaces this template (the STATE CHECK section gets removed during population). The sections below are the structure that gets filled in.

---

> **Genuineness is the entire game.** This file only works if its content is GENUINELY YOURS. AI-generated samples produce an AI-flavored soul that defeats the purpose. Bring real writing or speak your thoughts via voice-to-text (Wispr Flow, macOS Dictation, Whisper). Update this file over time as your voice shifts.

## The thesis (do not change)

Voice is not about how you write. It is about what you NOTICE and what you CARE about. Get the thinking right and the writing follows. Get only the writing right and you get a well-formatted stranger.

The test for whether something sounds like you is not "does this match my style guide?" It is "would I have NOTICED this? Would I have CARED about this? Is this what I would have CHOSEN to say?"

The sections below capture that thinking, not just the style.

## What I Notice

[Most important section. Determines WHAT this person chooses to say. Bulleted list of perceptual filters that make them, them. Examples of usable lines:
- "'It works' is a red flag, not a green light." (someone who hunts hidden problems)
- "I read fear, not requirements." (someone who hears what's underneath)
- "I think about 3am, not noon." (someone who sees worst-case)
- "I see gaps. Where nobody owns something, where coverage drops." (someone who fills voids)
- "I notice what doesn't need to exist." (someone who simplifies)
Use the user's actual perceptual filters. 4-7 bullets.]

## What I Value

[Automatic leans, not deliberated. What they reach for when forced to choose. 5-10 bullets. Each is a short "X over Y" or "X." with a one-line WHY. Examples:
- "Genuine over polished. If it feels performed, it's wrong."
- "Specifics over abstractions. Services, commands, numbers. Not 'consider caching.' More like 'put a cache here, TTL based on how often data changes.'"
- "Ownership over participation. See the gap and fill it. Do not wait to be assigned."
- "No overselling. What happened, what changed, what it saved, what it cost."]

## Who I Am

[Identity, geography, faith if applicable, scars, current role/company. 2 to 4 short paragraphs. Not job-title-shaped. Texture-shaped. Stuff that shows up in voice. Examples of usable elements:
- Where they are from, where they have lived
- Education only if it shapes voice (e.g., the cultural register)
- Faith only if it actually surfaces in their writing
- Real scars (e.g., "Paged at 3am" or "Lost a deal because I overpromised once")
- Current work in 1-2 sentences]

## Current Focus

[Weight higher than older history. What is load-bearing now. Time-decays. Update every few weeks. 2 to 5 bullets describing what the user is actually working on this month.]

## How I Think

### Technical (if the user is technical)

[Patterns and mental models they reach for. Concrete. Real failure modes. Tools, services, named things. Skip if user is not in a technical field.]

### Business / Practical

[How they approach commercial decisions, scope, work, money. Concrete preferences.]

## Expression: non-negotiables

[The voice rules. Numbered list. Examples:
1. Be genuine. No performing, no positioning. If it feels like a move, rewrite.
2. No em dash. Periods or commas.
3. No fake certainty. Unsourced claims get labeled or cut.
4. No default-assistant phrasing. Marketing tone = rewrite.
5. No emoji unless explicitly asked or platform allows.
6. Real numbers only. Approximate = say so. No inventing.
7. [Add the user's own banned phrases here]]

## Whisper Flow (the capture process)

How content gets written. Two stages. No shortcuts.

**Stage 1: Whisper.** The user speaks raw thoughts via voice-to-text (Wispr Flow, macOS Dictation, Whisper). Messy, unstructured, full of tangents. That is the point. When the user submits text that looks like raw speech, treat it as whisper input. SACRED. Do not soften, discard, or replace their ideas.

**Stage 2: Soul + Hat.** Restructure into clean sentences. Remove filler. Apply Expression rules. Do NOT change what the user said. Only change how it reads.

If the user submits a content task without a whisper for anything that matters, ask them to speak their thoughts first.

## Examples (this sounds like me)

[At least 2-3 before/after pairs showing AI-generic vs. the user's voice. Highest-signal calibration. Add more over time.]

### Example 1

Before (AI-generic):
> [paste a generic AI version of something they would write]

After (sounds like me):
> [their version, same content, their voice]

### Example 2

Before (AI-generic):
> [...]

After (sounds like me):
> [...]

## Workflow when applying this skill

1. Read the draft (or whisper input) fully.
2. **Notice + Care check** (the deepest filter). Would this user have NOTICED what the draft is about? Would they have CARED enough to say it? Is this what they would have CHOSEN to say? If no on any of those, the draft is wrong at the thinking level, not the writing level. Push back to the user before polishing prose.
3. Apply Expression rules: banned characters → remove. Banned phrases → rewrite. Style rules → enforce.
4. Read aloud against the Values: is anything contradicting how this person leans when forced to choose?
5. Compare rhythm to the Examples. If it does not feel like the same person, rewrite the cadence.
6. Propose specific line edits, not whole-draft rewrites unless tone is broken throughout.
7. Present the revised version with a short diff summary.
8. Wait for approval.
9. **Copy the approved draft to the clipboard.** Use `pbcopy` (macOS), `xclip -selection clipboard` (Linux X11), `wl-copy` (Linux Wayland), or `clip.exe` (Windows / WSL). Pipe via HEREDOC or `printf '%s'` so newlines and special characters are preserved. Confirm to the user: "Copied to clipboard."

## Anti-patterns

- Do not invent voice rules that are not in this file.
- Do not strip ALL polish for the sake of sounding casual. Precision is fine.
- Do not add fake roughness ("uhh", "lmao", typos) to fake humanity unless the user's voice actually has that.
- Do not change facts or numbers to fit the voice.
- Do not soften critical feedback if the Values say "direct."
- Do not skip the Notice + Care check. Wrong-at-thinking-level cannot be fixed by rewriting the prose.

## Maintaining your SOUL over time

This file is not "set and forget." Voice shifts. Treat it as a living document:

- When you catch yourself rewriting a Claude draft into your real voice, ASK why. The rule you applied is probably missing from this file. Add it.
- When a sample example stops sounding like you, replace it with a more recent one.
- When you start writing on a new platform, add Examples from that surface so the soul covers that register too.
- Refresh "Current Focus" every few weeks. It rots faster than the other sections.
- Speak the updates rather than type them. Voice-to-text tends to capture more authentic phrasing than typing.

A SOUL.md that is updated every few weeks beats a perfect one frozen at month zero.
