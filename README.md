# Claude Code Skills

A practitioner's collection of [Claude Code skills](https://code.claude.com/docs/en/skills) plus reusable templates for building your own. Curated from a working set of 20+ skills I use daily across engineering, writing, and consulting workflows.

## What's here

| Path | Type | Purpose |
|---|---|---|
| `skills/deslop/` | Concrete skill | Universal pass for catching AI-generated tells in text drafts before publishing |
| `skills/voice-hat-template/` | Template | Skeleton for encoding YOUR voice rules into an invocable skill |
| `skills/platform-hat-template/` | Template | Skeleton for platform-specific writing voices (LinkedIn, Reddit, Slack, etc.) |

More templates and concrete skills will land here as they get cleaned up for public release.

## How to use

1. Clone or copy a skill directory into your local `~/.claude/skills/` folder.
2. Open the `SKILL.md` and adjust the `description` frontmatter so Claude knows when to load it.
3. If it's a template, fill in the placeholders with YOUR voice rules, banned phrases, or platform conventions.
4. Restart Claude Code or use the `Skill` tool to invoke it.

Skills load into your CURRENT Claude Code context. They are not subagents. For when to use one vs the other, see the [Claude Code subagents docs](https://code.claude.com/docs/en/subagents) and the lessons below.

## Why templates instead of the original skills

Most of my skills encode MY voice (specific banned phrases, a personal blocklist of AI tells, a particular tone). Publishing them as-is would make other people sound like me, which is not useful for them. The templates here are voice-agnostic skeletons. You bring the rules, the skeleton enforces them.

The one concrete skill that IS publishable as-is is `deslop`, because the AI-tell catalog (sentence rhythm, vocabulary clusters, structural patterns) is universal across writers.

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

If you use Claude for ANY public-facing writing (emails, posts, proposals, README files), a personal voice skill pays for itself within a week. The voice rules in this repo's templates exist because LLMs default to a corporate, hedged, em-dash-heavy register that does not sound like any real person.

### Test the negative case

When writing a skill, also write down what the skill should NOT trigger on. Then verify Claude actually skips those cases. Skills that trigger too eagerly get disabled, skills that never trigger get forgotten.

### Layer skills, don't merge them

I have a universal `deslop` skill for general AI-tells AND a `reddit-deslop` skill that adds Reddit-specific failure modes (over-formatted, opening with "TL;DR", etc.). They compose. One mega-skill would be worse than two focused skills you can invoke together.

## Contributing

If you build a template you think belongs here, open a PR. Templates only, no personalized voice rules. The bar is: useful to anyone trying to build a similar skill, not just useful to me.

## License

MIT. See [LICENSE](./LICENSE).

## Author

Built and maintained by Mohamed ShehabEldin ([@muddahany](https://github.com/muddahany)) at [MSCLOUDTECH OÜ](https://mscloudtech.io). Senior backend and cloud engineer shipping AI-augmented products solo with Claude Code.
