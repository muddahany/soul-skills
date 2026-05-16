---
name: soul
description: Use whenever drafting any external-facing text in the user's personal voice. ALWAYS load when the user is composing emails, social posts, proposals, comments, profile bios, cover letters, replies, DMs, README files, or any author-attributed writing. Trigger on requests like "write a post about X", "draft an email", "help me reply", "write in my voice", "compose this", "as me", or any first-person writing task. Encodes the user's voice rules, banned phrases, required style, and values that shape voice. MUST be populated via the interactive onboarding in claude-code-skills/CLAUDE.md before it works; until populated, this skill should remind the user to run the onboarding flow.
---

# Soul

> **NOT YET POPULATED.** This file is the template structure. To fill it in, point your Claude Code at the onboarding flow at the root of the claude-code-skills repo. Claude will ask you to share writing samples and/or answer questions, then draft a populated version of this file for you to review.
>
> Once populated, remove this callout.

> **Genuineness is the entire game.** This file only works if its content is GENUINELY YOURS. AI-generated samples produce an AI-flavored soul that defeats the purpose. Bring real writing or speak your thoughts via voice-to-text (Wispr Flow, macOS Dictation, Whisper). Update this file over time as you notice your voice shifting or as new examples reveal rules that were not in the original draft.

## Identity

[ONE PARAGRAPH about who you are AS A WRITER. Not job title or resume. Examples of usable identity statements:
- "Senior backend engineer who shipped systems for fintech and ticketing. Writes like an engineer talking to another engineer. Allergic to corporate hedging."
- "Solo founder writing technical content. Sounds like a smart, slightly skeptical friend explaining something at a bar."
- "Compliance lawyer who hates legalese. Writes the way she would explain a contract to her sister."]

## Voice rules

### Banned characters

[List punctuation/characters you NEVER want in your output. One line each with a brief reason if helpful.]

- em dash (—): use periods or commas instead
- [add your own]

### Banned phrases

[Phrases that should never appear. The ones that make you cringe.]

- [add yours]

### Required style rules

[Positive rules. What MUST be true of the output.]

- [add yours]

## Writing style

[ONE TO TWO PARAGRAPHS describing your tone in writing. Be specific. Read like real adjectives a friend would use to describe how you sound on paper.]

## Values that shape voice

[3-7 values or beliefs that ACTUALLY change how you write. Not generic life values. Stuff that makes you cringe vs. nod when reading other people's work. Examples:
- "Precision over politeness. I would rather be right and curt than vague and kind."
- "Numbers when I have them, silence when I don't. Faking confidence is worse than admitting uncertainty."
- "Skepticism by default. I assume the press release is wrong until shown otherwise."
- "Engineer-to-engineer register. I write FOR people who can detect hand-waving."]

## Examples of "this sounds like me"

[At least 2-3 before/after pairs showing AI-generic vs. your voice. These are the highest-signal calibration the file can carry. Add more over time.]

### Example 1

Before (AI-generic):
> [paste a generic AI version of something you'd write]

After (sounds like me):
> [your version]

### Example 2

Before (AI-generic):
> [...]

After (sounds like me):
> [...]

## Workflow when applying this skill

1. Read the draft fully.
2. Run through Voice rules: banned characters → search and remove. Banned phrases → search and rewrite. Required style → check each rule.
3. Read aloud against the Writing style paragraph. Does it sound like the Identity statement?
4. Sanity-check against the Values: is anything in the draft contradicting how this user approaches writing?
5. Compare the draft's rhythm to the Examples. If it does not feel like the same person wrote them, rewrite.
6. Propose specific line edits, not whole-draft rewrites unless tone is broken throughout.
7. Present the revised version with a short diff summary.
8. Wait for approval before treating the rewrite as final.
9. **Copy the approved draft to the clipboard.** Use `pbcopy` (macOS), `xclip -selection clipboard` (Linux X11), `wl-copy` (Linux Wayland), or `clip.exe` (Windows / WSL). Pipe via HEREDOC or `printf '%s'` so newlines and special characters are preserved. Confirm to the user: "Copied to clipboard."

## Anti-patterns

- Do not invent voice rules that are not in this file.
- Do not strip ALL polish for the sake of sounding casual. Precision is fine.
- Do not add fake roughness ("uhh", "lmao", typos) to fake humanity unless the Identity statement says that is the voice.
- Do not change facts or numbers to fit the voice.
- Do not soften critical feedback if the Writing style says "direct."

## Maintaining your SOUL over time

This file is not "set and forget." Voice shifts. Treat it as a living document:

- When you catch yourself rewriting a Claude draft into your real voice, ASK why. The rule you applied is probably missing from this file. Add it.
- When a sample example stops sounding like you, replace it with a more recent one.
- When you start writing on a new platform (Reddit, Substack, podcast notes), add Examples from that surface so the soul covers that register too.
- Speak the updates rather than type them. Voice-to-text (Wispr Flow, etc.) tends to capture more authentic phrasing than typing.

A SOUL.md that is updated every few weeks beats a perfect one frozen at month zero.
