# Claude Code Skills

A practitioner's collection of [Claude Code skills](https://code.claude.com/docs/en/skills), centered on a personalized voice primitive (`soul`) that gets populated interactively from your own writing samples or an interview. Curated from a working set of 20+ skills I use daily across engineering, writing, and consulting workflows.

## Why this repo exists

AI-generated content is everywhere and most of it is slop. The people winning are not pure prompt-generators. They are people with genuine thoughts who use AI to structure and ship faster.

This repo is for the second kind. The skills here AMPLIFY your voice. They do not replace it.

You have to put effort in. Specifically:

- **For SOUL:** bring REAL examples of your writing. AI-generated samples produce an AI-flavored soul that defeats the purpose. If typing is slow for you, use voice-to-text (Wispr Flow, macOS Dictation, Whisper, or anything similar) to capture raw thoughts faster than typing. Voice tends to surface authentic phrasing that typed answers smooth over.
- **For deslop:** it catches obvious AI patterns. If you publish without running it, you publish slop.
- **For derived hats:** they only work because your SOUL is genuine. Garbage in, garbage out.

Using AI to organize and structure your genuine thoughts is not laziness. That is productivity. Generating content from scratch with no human input IS laziness, and it shows. This repo is built for the first, not the second.

The bar: when someone reads your output, they should think "this person has something to say and used a tool to say it well," not "this person let a tool talk for them."

## What's here

| Path | Type | What it is |
|---|---|---|
| `skills/deslop/` | Universal skill | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/soul/` | Personalized skill, populated by Claude | Encodes YOUR voice, writing style, and values that shape your voice. The recommended core skill. |
| `skills/platform-hat-deriver/` | Meta-skill | Auto-generates platform-specific hats (LinkedIn, Reddit, Slack, etc.) from your populated SOUL. Run once per platform. |
| `skills/voice-hat-template/` | Manual template (escape hatch) | Raw skeleton if you prefer to write your own voice rules without the SOUL interactive interview. |
| `skills/platform-hat-template/` | Manual template (escape hatch) | Raw skeleton for platform rules. Most users should prefer `platform-hat-deriver`. |

## How to use

There are three install paths, in order of recommendation.

### Path 1 (recommended): clone and let Claude populate SOUL interactively

This is the highest-value path because it includes the interactive SOUL onboarding (sample mode, interview mode, or hybrid). You cannot get this through plugin install.

```bash
git clone https://github.com/muddahany/claude-code-skills.git
cd claude-code-skills
claude
```

Claude auto-reads [`CLAUDE.md`](./CLAUDE.md) and walks you through:

1. Installing `deslop` (one command, no customisation).
2. Setting up `soul` interactively. You pick one of three modes:
   - **Sample mode** — paste 5 to 10 examples of your real writing. Claude extracts patterns.
   - **Interview mode** — Claude asks 10 to 15 questions. Voice-to-text recommended (Wispr Flow, Whisper, macOS Dictation).
   - **Hybrid** — sample first, interview to fill gaps.
3. Reviewing and approving the populated `soul/SKILL.md`.
4. Installing it to `~/.claude/skills/soul/`.

Say "set this up for me" once Claude opens.

### Path 2: Claude Code plugin marketplace install

Fastest path if you only want `deslop` and the bare templates (skip the SOUL onboarding).

```
/plugin marketplace add muddahany/claude-code-skills
/plugin install deslop@muddahany-skills
```

Available plugins: `deslop`, `soul`, `platform-hat-deriver`, `voice-hat-template`, `platform-hat-template`.

If you install `soul` this way, it lands UNPOPULATED. You will need to fill it in manually or run the onboarding from Path 1 afterwards.

### Path 3: manual `cp -r` (for power users)

If you do not want plugins or the onboarding:

```bash
git clone https://github.com/muddahany/claude-code-skills.git
mkdir -p ~/.claude/skills
cp -r claude-code-skills/skills/deslop ~/.claude/skills/
cp -r claude-code-skills/skills/voice-hat-template ~/.claude/skills/
cp -r claude-code-skills/skills/platform-hat-template ~/.claude/skills/
```

Then edit each `SKILL.md` to fill in the `<<PLACEHOLDER>>` markers and rename the folders to your preference.

Skills load into your CURRENT Claude Code context. They are not subagents. For when to use one vs the other, see the [Claude Code subagents docs](https://code.claude.com/docs/en/subagents) and the lessons below.

## Why `soul` instead of hardcoded voice skills

Most published voice skills encode the AUTHOR's voice. Installing them makes you sound like that author, which is not what you want. The `soul` primitive flips that: it ships as a STRUCTURE, and Claude populates it from YOUR writing or YOUR answers. Same skill file shape, completely different content per user.

The downstream benefit: platform-specific hats (LinkedIn, Reddit, Slack, etc.) get DERIVED from your `soul` plus the platform's conventions using the `platform-hat-deriver` skill. One personalized source of truth, many platform-tuned outputs. Each derived hat is a thin delta on top of SOUL, so updates to your SOUL propagate.

## Universal patterns across these skills

Two conventions show up in every output-producing skill in this repo:

1. **Copy-to-clipboard as the final step.** Once you approve the output, Claude pipes it straight to your clipboard (`pbcopy` / `xclip` / `clip.exe`). No terminal-copying. Paste straight into Slack, LinkedIn, your editor, wherever.
2. **Platform syntax is treated as load-bearing.** When a skill targets a specific platform (LinkedIn, Reddit, Slack, etc.), the SKILL.md explicitly encodes that platform's syntax: markdown variant, bold/italic syntax, header support, mention format, hashtag handling, line-break behaviour, character limits. Generic "format constraints" is not enough; the platform syntax section is what keeps your output from rendering broken.

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

This repo is curated, not a dumping ground. See [CONTRIBUTING.md](./CONTRIBUTING.md) for the bar, the do/do-not list, and the quality checklist for new skills. TL;DR: universal skills and templates only, no personal voice rules, follow Anthropic's frontmatter guidance, use [`template/SKILL.md`](./template/SKILL.md) as the starting point.

## License

MIT. See [LICENSE](./LICENSE).

## Author

Built and maintained by Mohamed ShehabEldin ([@muddahany](https://github.com/muddahany)) at [MSCLOUDTECH OÜ](https://mscloudtech.io). Senior backend and cloud engineer shipping AI-augmented products solo with Claude Code.
