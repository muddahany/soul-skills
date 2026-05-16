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

The interview is structured around the deep framing: NOTICE, VALUE, WHO, FOCUS, THINK, EXPRESSION. The expression questions (banned phrases, punctuation, format) come at the END, not the start. Voice rules without the thinking behind them produce a hollow style guide.

Ask in this order, one or two questions at a time. Adapt. If an answer is short or AI-shaped, ask a followup ("can you say more?", "what's a specific example?").

### What I Notice (the perceptual filter)

1. "What do you notice that other people in your field tend to miss? What's the thing you spot first when you walk into a meeting / read a codebase / hear someone's pitch?"
2. "When someone describes a problem to you, what do you HEAR underneath the words? What signals do you read?"
3. "What kind of detail makes you stop and pay attention? What kind of detail bores you?"

### What I Value (automatic leans)

4. "When forced to choose, what do you reach for? Genuine vs polished? Building vs talking? Speed vs precision? Give 3 to 5 X-over-Y statements with a one-line reason for each."

### Who I Am (identity, not resume)

5. "Where are you from, where have you lived, what cultural register shows up in your writing?"
6. "Real scars: what hard things have you done that show up in voice? (3am pages, lost deals, failed projects, public corrections, etc.)"
7. "Faith, values, or beliefs that surface in writing. Skip if none."

### Current Focus (time-decays)

8. "What are you actually working on this month? 2 to 5 things that are load-bearing right now."

### How I Think

9. "If you are technical: what mental models, patterns, or tools do you reach for? Be concrete."
10. "How do you approach business or commercial decisions? Scope, money, work."

### Expression: voice rules (lowest priority but highest signal day-to-day)

11. "Which 3 to 5 phrases do you NEVER want to see in your own writing?"
12. "Any punctuation you want banned? (em dash, ellipses, etc.)"
13. "Do you use CAPS for emphasis? Bold? Italics? Or none?"
14. "Short paragraphs or long? Lead with result or build up to it? Hedge or state directly?"
15. "Casual or formal? Slang OK? Curse words OK?"

### Wrap

16. "What's an example of writing you have seen that made you cringe? Why?"
17. "What's an example of writing you have seen that made you nod? Why?"
18. "Anything platform-specific that matters now? (Reddit, LinkedIn, Slack DMs, etc.) We can derive platform hats later."

## Mode: HYBRID

Run SAMPLE first. Then ask only the INTERVIEW questions the samples did not answer.

## Draft the populated SOUL.md

Replace the template structure in `SKILL.md` with the user's actual content, in this order:

- **The thesis paragraphs** — keep as-is. Do not edit. They are the framing for everything else.
- **What I Notice** — 4 to 7 bulleted perceptual filters from question set 1. Each starts with a sharp observation in the user's words.
- **What I Value** — 5 to 10 X-over-Y bullets from question 4. Each with a one-line WHY.
- **Who I Am** — 2 to 4 short paragraphs synthesised from questions 5 to 7. Texture, not resume.
- **Current Focus** — from question 8. Date-stamp it ("As of [month/year]") so the user knows when to refresh.
- **How I Think** — Technical and Business subsections from questions 9 and 10.
- **Expression: non-negotiables** — numbered list combining default rules (no em dash, no fake certainty, no emoji unless asked, real numbers only) plus the user's specific bans from questions 11 to 15.
- **Whisper Flow** — keep as-is.
- **Examples** — at least 2 before/after pairs. Use real samples if provided (paraphrased if sensitive). Otherwise generate plausible ones and ask the user to confirm.

Tag uncertain extractions `[verify]` so the user can spot-check.

**Important:** Remove the "STATE CHECK" section from SKILL.md (it is no longer needed once populated). Keep the references/onboarding.md file on disk in case the user wants to re-run the onboarding later.

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
