# Soul Skills

[Claude Code](https://code.claude.com/docs/en/skills) skills that AMPLIFY your genuine voice instead of generating a fake one. Anchored by `soul`, a personalized voice primitive populated interactively from your own writing samples or an interview.

## Install

```
/plugin marketplace add muddahany/soul-skills
/plugin install everything@soul-skills
/reload-plugins
/welcome
```

`/welcome` prints the next steps. The most important one is `/soul`, which walks you through populating your SOUL interactively (sample mode, interview mode, or hybrid).

If you prefer to clone and run from the repo, see [CLAUDE.md](./CLAUDE.md). The onboarding flow auto-loads when Claude Code starts in this directory.

## What's here

| Path | Type | What it is |
|---|---|---|
| `skills/soul/` | Personalized core | Encodes YOUR voice (perceptual filters, values, identity, current focus, expression rules). Self-onboards on first use. |
| `skills/deslop/` | Universal | Catches AI-generated tells in any text draft. Install as-is. |
| `skills/whisper-flow/` | Input pipeline | Listens to YOU. Takes raw voice-to-text dictation and restructures into clean prose without changing your ideas. |
| `skills/read-incoming/` | Input pipeline | Listens to OTHERS. Processes incoming messages (long emails, RFPs, threads, support tickets) and extracts the real ask, the underlying fear, implicit constraints, and a recommended response shape. |
| `skills/platform-hat-deriver/` | Meta-skill | Auto-derives platform hats (LinkedIn, Reddit, Slack, etc.) from your SOUL. Built-in syntax reference for 8 platforms. |
| `skills/voice-hat-template/` | Manual escape hatch | Raw skeleton if you skip the SOUL onboarding. |
| `skills/platform-hat-template/` | Manual escape hatch | Raw skeleton if you skip the deriver. |
| `commands/welcome.md` | Slash command | `/welcome` shows next steps after install. |
| `commands/diagnose.md` | Slash command | `/diagnose` audits the state of every soul-skill on your machine. |
| `examples/` | Reference | Sanitized populated SOUL example so you can see what "done" looks like. |
| `template/SKILL.md` | Contributor template | Skeleton for adding a new generic skill. |

## How it composes

```
[incoming message]                 [your voice]
       │                                │
       ▼                                ▼
  read-incoming                   voice-to-text
       │                                │
       ▼                                ▼
     BRIEF                         whisper-flow
       │                                │
       └─────► (you react) ◄────────────┘
                    │
                    ▼
                 soul              (applies your voice)
                    │
                    ▼
            <platform>-hat        (platform syntax, hard limits, AI-detection)
                    │
                    ▼
                 deslop           (final universal AI-tell pass)
                    │
                    ▼
            copy to clipboard
```

Two input pipelines: `read-incoming` for what others send you, `whisper-flow` for what you say. Both feed into the same voice/platform/clean output pipeline. Every output-producing skill ends with a clipboard copy. You paste straight into Slack, LinkedIn, your editor, wherever.

## Why this exists

AI-generated content is everywhere and most of it is slop. The people winning are not pure prompt-generators. They are people with genuine thoughts who use AI to structure and ship faster.

You have to put effort in. SOUL only works if its content is GENUINELY YOURS. AI-generated samples produce an AI-flavored SOUL that defeats the purpose. If typing is slow, use voice-to-text (Wispr Flow, macOS Dictation, Whisper). Voice surfaces authentic phrasing typed answers smooth over.

Using AI to organize your real thoughts is productivity. Generating content from scratch with no human input is laziness, and it shows.

## Contributing

This repo is curated, not a dumping ground. Universal skills and templates only, no personal voice rules. See [CONTRIBUTING.md](./CONTRIBUTING.md). Start from [`template/SKILL.md`](./template/SKILL.md).

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).

## License

MIT. See [LICENSE](./LICENSE).

## Author

[Mohamed ShehabEldin](https://github.com/muddahany) at [MSCLOUDTECH OÜ](https://mscloudtech.io).
