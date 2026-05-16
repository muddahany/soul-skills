---
name: whisper-flow
description: Use whenever the user submits raw, unstructured, stream-of-thought text (typically from voice-to-text tools like Wispr Flow, macOS Dictation, Whisper) that needs to be restructured into clean publishable writing WITHOUT changing the ideas. ALWAYS load if the input has run-on sentences, sentence fragments, repeated tangents, or other hallmarks of dictation. Trigger phrases: "here are my raw thoughts", "I whispered this", "polish this dictation", "clean up this transcript", "restructure but do not change my ideas", "I dictated this", or any input that obviously looks like raw speech-to-text. The two-stage pipeline: Stage 1 (Whisper) is sacred user input; Stage 2 (Soul + Hat) restructures cadence and applies voice rules without changing meaning. Final step copies the polished output to the clipboard.
---

# Whisper Flow

## The thesis

Voice-to-text is the fastest way to capture genuine thoughts. Typing slows people down and smooths their voice into something that does not sound like them. Speaking surfaces authentic phrasing, real emphasis, and the specific examples that make writing land.

The cost: raw speech-to-text looks bad on the page. Run-ons, half-thoughts, tangents, fillers ("uhh", "like", "you know"), repetition. This skill bridges raw whisper to publishable text in two stages.

**Hard rule:** the user's IDEAS are sacred. Only the prose around them changes.

## When to use

- User pastes obviously-raw dictation, transcript, or stream-of-thought.
- User says "I whispered some thoughts" or names a voice-to-text tool.
- User asks to "clean up" or "restructure" text they spoke.
- Input has fragments, run-ons, fillers, or tangents that signal speech-to-text.
- Used as an INPUT pipeline for soul + platform hat. Whisper-flow runs first, then soul applies voice, then a platform hat applies platform-specific format.

## When NOT to use

- User wrote the text by typing. They probably already structured it.
- User wants a fresh draft generated, not a restructure. (Use soul or a hat directly.)
- Text is already clean and just needs voice polish. (Use deslop instead.)

## The two stages

### Stage 1: Whisper (sacred user input)

The raw text from the user. Do NOT discard, soften, replace, or "interpret" any idea in it. Treat every claim, example, opinion, tangent, and number as load-bearing until proven otherwise.

If something looks contradictory, ASK the user. Do not silently resolve.

If something looks unclear, ASK the user. Do not paraphrase.

### Stage 2: Soul + Hat (restructure only)

Your job in this stage:

1. Identify all the IDEAS in the whisper (one per claim, observation, example, or argument).
2. Remove only:
   - Filler words ("uhh", "like", "you know", "I mean", "basically")
   - Repeated phrasing of the same idea (keep the strongest phrasing)
   - Dead ends and abandoned half-thoughts (only if abandoned; preserve if the user comes back to them)
3. Restructure remaining ideas into clean sentences with varied rhythm.
4. Apply the user's `soul` skill voice rules (banned characters, banned phrases, required style, values).
5. If a target platform was specified, apply the relevant platform hat on top (format, syntax, length, AI detection checklist).

Do NOT:
- Add new ideas the user did not express.
- Change facts, numbers, or claims.
- Smooth out sharp opinions the user expressed clearly.
- Soften critical takes if soul says "direct."
- Compress two related ideas into one if both were distinct in the whisper.

## Workflow

1. **Confirm this is whisper input.** If unclear, ask: "Is this a raw dictation or did you type this?" If typed, route to soul/deslop instead.
2. **Read the whisper fully.** Do not start rewriting partway through.
3. **List the ideas** internally before rewriting. This forces you to identify what is load-bearing.
4. **Confirm target platform if any.** Ask: "Where is this going? (LinkedIn / Reddit / blog / Slack / email / cold email / generic)."
5. **Restructure cadence.** Break run-ons, group related ideas, vary sentence length.
6. **Apply `soul`** if installed and populated. Banned characters, phrases, style.
7. **Apply platform hat** if target platform was specified and a hat exists. Format, syntax, length norms.
8. **Run AI-detection checklist** from the platform hat (if applicable) or from `deslop` (if generic).
9. **Present revised version + idea-preservation check.** Tell the user explicitly which ideas you preserved and which (if any) you cut as filler. Let them push back.
10. **Wait for approval.**
11. **Copy the approved draft to the clipboard.** Use `pbcopy` (macOS), `xclip -selection clipboard` (Linux X11), `wl-copy` (Linux Wayland), or `clip.exe` (Windows / WSL). Pipe via HEREDOC or `printf '%s'` so newlines and special characters are preserved. Confirm: "Copied to clipboard."

## Output format

```
## Ideas extracted from whisper

1. [idea 1, as the user expressed it]
2. [idea 2]
3. [...]

## What I cut as filler (if anything)

- [filler / dead-end the user can confirm should stay cut]

## Restructured draft

[Clean, voice-applied, platform-tuned text]

## What changed
- [Cadence: broke X run-ons into Y sentences]
- [Voice: removed banned phrase Z]
- [Platform: converted markdown to <platform variant>]
```

After approval, the clipboard copy step runs.

## Anti-patterns

- Do NOT paraphrase. Use the user's words wherever possible.
- Do NOT smooth sharp opinions. If the user said "this is dumb," do not soften to "this could be improved."
- Do NOT skip Stage 1 mental check. If you start rewriting before listing ideas, you will lose some.
- Do NOT compress related ideas into one polished sentence if the user expressed them as two distinct thoughts.
- Do NOT add transitional sentences that contain new claims. "This matters because X" introduces X. Only restate what the user said.
- Do NOT apply platform formatting if the user did not specify a target platform. Default to generic clean prose.

## Composition with other skills

Whisper Flow is the INPUT pipeline. It composes with:

- **`soul`** — applies the user's personal voice on top of the restructured cadence.
- **`<platform>-hat`** — applies platform-specific syntax, length, failure modes, AI detection.
- **`deslop`** — generic AI-tell catcher when no platform hat exists.

Recommended order: Whisper Flow → soul → platform hat → deslop (final pass) → clipboard.

## Tips

- The more the user dictates over time, the better Claude gets at identifying their natural rhythm and emphasis. Encourage them to whisper rather than type for anything that matters.
- If the user has multiple whisper sessions on the same topic, ask whether to MERGE them (preserving all ideas from both) or use only the latest.
- For long whispers (10+ minutes of dictation), summarise the idea list back to the user BEFORE restructuring. Confirms you caught everything.
