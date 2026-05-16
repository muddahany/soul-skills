# Claude Code Skills

A practitioner's collection of [Claude Code skills](https://code.claude.com/docs/en/skills), centered on a personalized voice primitive (`soul`) that gets populated interactively from your own writing samples or an interview. Curated from a working set of 20+ skills I use daily across engineering, writing, and consulting workflows.

## Why this repo exists

AI-generated content is everywhere and most of it is slop. The people winning are not pure prompt-generators. They are people with genuine thoughts who use AI to structure and ship faster.

This repo is for the second kind. The skills here AMPLIFY your voice. They do not replace it.

You have to put effort in. Specifically:

- **For SOUL:** bring REAL examples of your writing. AI-generated samples produce an AI-flavored soul that defeats the purpose. If typing is slow for you, use voice-to-text (Wispr Flow, macOS Dictation, Whisper, or anything similar) to capture raw thoughts faster than typing. Voice tends to surface authentic phrasing that typed answers smooth over.
- **For deslop:** it catches obvious AI patterns. If you publish without running it, you publish slop.
- **For derived hats (V2):** they only work because your SOUL is genuine. Garbage in, garbage out.

Using AI to organize and structure your genuine thoughts is not laziness. That is productivity. Generating content from scratch with no human input IS laziness, and it shows. This repo is built for the first, not the second.

The bar: when someone reads your output, they should think "this person has something to say and used a tool to say it well," not "this person let a tool talk for them."

## What's here

| Path | Type | What it is |
|---|---|---|
| `skills/deslop/` | Universal skill | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/soul/` | Personalized skill, populated by Claude | Encodes YOUR voice, writing style, and values that shape your voice. The recommended core skill. |
| `skills/voice-hat-template/` | Manual template (escape hatch) | Raw skeleton if you prefer to write your own voice rules without an interactive interview. |
| `skills/platform-hat-template/` | Manual template (escape hatch) | Raw skeleton for platform-specific writing rules. A `platform-hat-deriver` is planned for V2. |

## How to use

### Recommended: let Claude install and populate for you

Clone this repo, open Claude Code in the directory, and Claude will auto-read [`CLAUDE.md`](./CLAUDE.md) and walk you through:

1. Installing `deslop` (one command, no customisation).
2. Setting up `soul` interactively. You pick one of three modes:
   - **Sample mode** — paste 5 to 10 examples of your real writing. Claude extracts patterns.
   - **Interview mode** — Claude asks 10 to 15 questions about how you write.
   - **Hybrid** — sample first, interview to fill gaps. Recommended.
3. Reviewing and approving the populated `soul/SKILL.md`.
4. Installing it to `~/.claude/skills/soul/`.

```bash
git clone https://github.com/muddahany/claude-code-skills.git
cd claude-code-skills
claude
```

Then say "set this up for me" or just describe what you want. The onboarding file does the rest.

### Manual install (for power users)

If you'd rather write your voice rules by hand:

```bash
mkdir -p ~/.claude/skills
cp -r skills/deslop ~/.claude/skills/
cp -r skills/voice-hat-template ~/.claude/skills/
cp -r skills/platform-hat-template ~/.claude/skills/
```

Then edit each `SKILL.md` to fill in the `<<PLACEHOLDER>>` markers and rename the folders to your preference.

Skills load into your CURRENT Claude Code context. They are not subagents. For when to use one vs the other, see the [Claude Code subagents docs](https://code.claude.com/docs/en/subagents) and the lessons below.

## Why `soul` instead of hardcoded voice skills

Most published voice skills encode the AUTHOR's voice. Installing them makes you sound like that author, which is not what you want. The `soul` primitive flips that: it ships as a STRUCTURE, and Claude populates it from YOUR writing or YOUR answers. Same skill file shape, completely different content per user.

The downstream benefit: platform-specific hats (LinkedIn, Reddit, Slack, etc.) can be DERIVED from your `soul` plus the platform's conventions. One personalized source of truth, many platform-tuned outputs. The deriver is planned for V2 of this repo.

## What goes in `soul`

The populated `soul/SKILL.md` has these sections:

- **Identity** — one paragraph about who you are as a writer.
- **Voice rules** — banned characters, banned phrases, required style rules.
- **Writing style** — 1 to 2 paragraphs of tone.
- **Values that shape voice** — 3 to 7 values that genuinely change how you write (precision over politeness, numbers when you have them, etc.).
- **Examples** — before/after pairs showing AI-generic vs. your voice.

Target length: 50 to 80 lines. Tight enough to load on every voice-related conversation without bloating context.

## Lessons from building 20+ skills

Things I wish someone had told me earlier.

### Skill vs subagent: pick by context cost

A skill loads into your current conversation. Its full body stays in context. Good for: checklists, voice rules, workflow templates, anything you reference repeatedly.

A subagent runs in its OWN context window. Returns a summary. Good for: research that generates noise (logs, file scans), tasks with different tool access, work that would bloat your main session with 50+ file reads.

Wrong choice = wasted tokens or polluted context. Skills look cheap but a 2,000-line skill loaded into every turn is not cheap. Subagents look heavy but they keep your main window clean.

### The description field is the most important line

Claude's auto-trigger reads the `description` in frontmatter to decide whether to load the skill. Generic descriptions get ignored. Be aggressively specific about the triggering verbs and contexts.

Bad: `description: Helps with code review`
Good: `description: Use when reviewing a pull request, when the user says "review this PR", or when asked to inspect a code change for issues before merge`

### Keep skills focused

A skill that tries to do five things gets loaded only when Claude is confident about all five. A skill that does one thing well gets loaded reliably.

If a skill grows past ~300 lines, consider splitting it. Long skills bloat every conversation that triggers them.

### Voice skills compound

If you use Claude for ANY public-facing writing (emails, posts, proposals, README files), a personalised voice skill pays for itself within a week. The default LLM register (corporate, hedged, em-dash-heavy) does not sound like any real person.

### Test the negative case

When writing a skill, also write down what the skill should NOT trigger on. Then verify Claude actually skips those cases. Skills that trigger too eagerly get disabled, skills that never trigger get forgotten.

### Layer skills, don't merge them

I have a universal `deslop` skill for general AI-tells AND a personalised `soul` for voice. They compose. One mega-skill would be worse than two focused skills you can invoke together.

## Contributing

If you build a generic template or universal skill you think belongs here, open a PR. Personal voice skills do not belong in this repo. The bar is: useful to anyone trying to build a similar skill, not just useful to you.

## License

MIT. See [LICENSE](./LICENSE).

## Author

Built and maintained by Mohamed ShehabEldin ([@muddahany](https://github.com/muddahany)) at [MSCLOUDTECH OÜ](https://mscloudtech.io). Senior backend and cloud engineer shipping AI-augmented products solo with Claude Code.
