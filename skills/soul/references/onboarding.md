# SOUL Onboarding Flow

> Load this file when `SKILL.md` detects the "NOT YET POPULATED" callout. Run the flow below interactively with the user, then overwrite `~/.claude/skills/soul/SKILL.md` with the populated version.

## Genuineness gate (state this first)

Before anything else, tell the user:

> "Setting up SOUL takes 20 to 40 minutes done well. The output is only as good as the input. If you have voice-to-text (Wispr Flow, macOS Dictation, Whisper), use it: spoken answers expose authentic phrasing that typed ones smooth over. Are you ready to do this now? If you're in a rush, come back later. Half-effort SOUL is worse than no SOUL."

If they want to defer, stop. Tell them to run `/soul` or say "set up my SOUL" later.

## Mode selection

Present three options. Do not default. Add a transparency note: anything they share goes through their Claude Code session.

1. **Sample mode** — user pastes 5 to 10 examples of REAL writing. Highest fidelity but needs samples on hand.
2. **Interview mode** — Claude asks 10 to 15 questions. Slower but no samples needed.
3. **Hybrid** — sample first, interview fills gaps. Recommended.

Let the user pick.

## Mode: SAMPLE

1. **Explicitly ask:** "Are these samples GENUINELY YOUR writing, not AI-generated or AI-edited?" If unsure or admitted AI-touched, switch to INTERVIEW mode. AI samples pollute the soul.
2. Ask for 5 to 10 examples. Variety helps: blog post, Slack message, cold email, Reddit comment, etc.
3. Read every sample. Extract patterns across:
   - **Banned characters** (em dashes, ellipses, etc.)
   - **Banned phrases** (clichés, filler, AI-tells they avoid)
   - **Required style rules** (CAPS for emphasis, lead-with-result, short paragraphs, etc.)
   - **Tone** (one paragraph of texture)
   - **Values that show up** (precision, skepticism, anti-corporate, etc.)
4. Tag uncertain extractions `[verify with user]` so they spot-check.

## Mode: INTERVIEW

Recommend voice-to-text up front: "Speak your answers via Wispr Flow or similar. Spoken answers expose authentic phrasing typed ones smooth over."

Ask these in order, one or two at a time. Adapt. If an answer is short or AI-shaped, ask a followup ("can you say more?", "what's a specific example?").

1. "How would you describe how you sound in writing in one sentence? A friend describing you."
2. "Which 3 to 5 phrases do you NEVER want to see in your own writing?"
3. "Any punctuation you want banned?" (em dash is common)
4. "Do you use CAPS for emphasis? Bold? Italics? Or none?"
5. "Short paragraphs or long ones?"
6. "Do you lead with the result or build up to it?"
7. "Do you hedge ('might', 'could', 'perhaps') or state directly?"
8. "How casual or formal? Slang OK? Curse words OK?"
9. "Do you use lists/bullets a lot or mostly flowing prose?"
10. "What's an example of writing you have seen that made you cringe? What was wrong with it?"
11. "What's an example of writing you have seen that made you nod? What was right about it?"
12. "Are there 2 to 3 values you hold that change how you write? (precision over politeness, numbers when you have them, skepticism by default, etc.)"
13. "Anything platform-specific that matters? (Reddit comments, LinkedIn posts, Slack DMs, etc.)"

## Mode: HYBRID

Run SAMPLE first. Then ask only the INTERVIEW questions the samples did not answer.

## Draft the populated SOUL.md

Replace the template structure in `SKILL.md` with the user's actual content:

- **Identity paragraph** — one paragraph in the user's voice about who they are AS A WRITER. Not job title.
- **Banned characters** — bullet list with brief reasons.
- **Banned phrases** — their actual list.
- **Required style rules** — positive rules they care about.
- **Writing style paragraph** — 1 to 2 paragraphs of tone description.
- **Values that shape voice** — 3 to 7 values. Only ones that actually change writing.
- **Examples** — at least 2 before/after pairs. Use real samples if provided (paraphrased if sensitive). Otherwise generate plausible ones and ask user to confirm.

Tag uncertain rules `[verify]` so the user can spot-check.

**Important:** Remove the "NOT YET POPULATED" callout at the top. Also remove the STATE CHECK section from SKILL.md (it is no longer needed once populated). Keep the references/onboarding.md file on disk in case the user wants to re-run the onboarding later.

## Review with the user

Display the full populated SOUL.md. Ask:
- "Does this sound like you?"
- "Anything missing?"
- "Anything wrong?"

Iterate until the user is happy. Be willing to rewrite sections that miss.

## Install

Write the final SOUL.md to `~/.claude/skills/soul/SKILL.md`. If the user is running this from inside the soul-skills repo clone, also offer to commit the change locally so they don't lose it.

## After SOUL is installed

Offer the next step:

> "Your SOUL is set up. If you write on specific platforms (LinkedIn, Reddit, Slack, etc.) and want a hat tuned to each, I can derive one now using the `platform-hat-deriver` skill. One platform at a time. Want to do that?"

If yes, the platform-hat-deriver skill (which should be installed alongside soul) takes over.

## Anti-patterns during onboarding

- Do not push through if the user says they are in a rush.
- Do not accept AI-generated writing samples. Switch to interview mode.
- Do not write rules the user did not actually express. Ask followups instead of fabricating.
- Do not batch-generate platform hats after onboarding. One at a time.
- Do not skip the genuineness gate at the top.
