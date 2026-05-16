---
name: welcome
description: Show what was just installed from soul-skills and the next steps in order. Run this right after installing the plugin. Triggers on /welcome, "what now", "what should I do next", "I just installed soul-skills", "how do I use this".
---

# Welcome to soul-skills

You just installed the **soul-skills** plugin. Here is what is available and what to do next.

## What you have now

| Skill | Status | What it does |
|---|---|---|
| `deslop` | Ready | Universal AI-tell catcher. Works as-is on any text draft. |
| `soul` | **NEEDS SETUP** | Personal voice primitive. Ships unpopulated. Drives all "write as me" workflows. |
| `whisper-flow` | Ready | Listens to YOU. Restructures voice-to-text dictation into clean prose without changing your ideas. |
| `read-incoming` | Ready | Listens to OTHERS. Processes long emails, RFPs, threads, support tickets and extracts the real ask + recommended response shape. |
| `platform-hat-deriver` | Ready (needs SOUL) | Auto-generates platform-specific hats (LinkedIn, Reddit, Slack, etc.) from your SOUL. |
| `voice-hat-template` | Manual escape hatch | Raw skeleton. Use only if you skip SOUL. |
| `platform-hat-template` | Manual escape hatch | Raw skeleton. Use only if you skip the deriver. |

## Next steps, in order

### Step 1: Set up your SOUL (the high-leverage step)

Without this, the platform-hat-deriver cannot run and Claude has no idea how you sound on paper.

Just say one of these:

```
/soul
```

or

```
set up my SOUL
```

Claude will:
1. Ask you to pick a mode (sample / interview / hybrid). Voice-to-text recommended.
2. Walk you through 13 questions OR analyse 5 to 10 of your real writing samples.
3. Draft a populated `soul/SKILL.md` for you to review.
4. Install the populated version to `~/.claude/skills/soul/SKILL.md`.

Takes 20 to 40 minutes done well. Half-effort SOUL is worse than no SOUL, so block the time.

### Step 2: Test deslop on a real draft

Once you have something to publish (an email, a post, a Reddit comment), say:

```
deslop this draft
```

and paste the text. Claude will flag AI-tells, propose rewrites, and copy the clean version to your clipboard.

### Step 3: Derive your first platform hat (after SOUL is populated)

Pick the platform you write on most. Say:

```
create a LinkedIn hat for me
```

(or Reddit, Slack, Discord, Twitter, GitHub, Substack, email)

The deriver looks up the platform's syntax from its built-in reference, asks you 4 personal questions, then writes a `~/.claude/skills/<platform>-hat/SKILL.md` tuned to that surface.

## Got it. Now what?

If you have 20 to 40 minutes free right now, run `/soul` and let's set up your voice. If not, bookmark this and come back. Half-effort SOUL is worse than no SOUL.

## Questions or feedback

- Repo: https://github.com/muddahany/soul-skills
- Issues: https://github.com/muddahany/soul-skills/issues
- Philosophy: AI should AMPLIFY your genuine voice, not generate fake voice. Effort in, signal out.
