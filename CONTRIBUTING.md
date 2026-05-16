# Contributing

This repo is curated, not a dumping ground. The bar is high. Read this before opening a PR.

## What belongs here

- **Universal skills** like `deslop` that work for any user without customisation.
- **Templates** for skills that need per-user customisation (voice, platform, etc.). Templates use `<<PLACEHOLDER>>` markers and ship unpopulated.
- **Improvements to the SOUL onboarding flow** (better interview questions, smarter sample extraction logic, better edge-case handling).
- **Documentation** explaining why a skill exists, when to use it, and when not to.

## What does NOT belong here

- **Personal voice skills.** If your skill encodes YOUR phrases, YOUR tone, YOUR cringe list, it belongs in your own repo or your local `~/.claude/skills/`, not here.
- **Client-specific or organisation-specific skills.** No "MyCompany's PR workflow" or "ATG-style Jira ticket creation." Generalize or skip.
- **Roleplay character skills.** Out of scope.
- **Skills that duplicate existing widely-used ones** without a clear differentiator.
- **Mega-skills that try to do five things at once.** Split into focused single-purpose skills.

## Quality bar for new skills

Before opening a PR, your skill should:

- [ ] Have a SKILL.md with a `name` (kebab-case) and a `description` in YAML frontmatter.
- [ ] Description states WHAT the skill does AND WHEN it should trigger, with specific trigger phrases. Be assertive. See Anthropic's official guidance: descriptions are the primary triggering mechanism.
- [ ] SKILL.md body under 500 lines. Split into `references/` if it grows past that.
- [ ] Imperative voice ("Do X", not "This skill does X").
- [ ] At least one "When to use" and one "When NOT to use" section. The negative case matters.
- [ ] Use the [`template/SKILL.md`](./template/SKILL.md) as your starting point.
- [ ] Pass a manual test: load it into a fresh `~/.claude/skills/` install and verify it triggers when you expect AND skips when you do not.

## Style rules

- No em dashes. Use periods or commas.
- No emoji unless explicitly required by the skill's domain.
- Real numbers only. If you do not have data, do not invent it.
- Explain the WHY behind rules. Avoid excessive ALL-CAPS MUST/NEVER patterns. Anthropic's official guidance calls these a "code smell" indicating overly rigid specification.
- Kebab-case for skill folder names and `name:` field.
- **If a skill produces text the user will publish or send, the last workflow step MUST copy the output to the clipboard** (`pbcopy` on macOS, `xclip -selection clipboard` on Linux X11, `wl-copy` on Wayland, `clip.exe` on Windows / WSL). Users should not have to terminal-copy.
- **If a skill targets a specific platform** (LinkedIn, Reddit, Slack, etc.), include a `## Platform syntax` section in the SKILL.md that explicitly lists markdown support, bold/italics syntax, header support, code block support, mention syntax, hashtag handling, line-break behaviour, and any character limit. Each platform has its own rendering rules and skipping this section produces visually broken output.

## How to submit

1. Fork the repo.
2. Add your skill to `skills/<your-skill-name>/SKILL.md` following the template.
3. If your skill should be installable via plugin marketplace, add an entry to `.claude-plugin/marketplace.json` (alphabetical order, by `name`).
4. Open a PR with a short description: what it does, who it is for, why it belongs in a curated repo.

## License

By contributing, you agree your contributions are MIT-licensed under the terms of [LICENSE](./LICENSE).
