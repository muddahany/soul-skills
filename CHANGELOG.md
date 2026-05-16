# Changelog

All notable changes to soul-skills.

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/).

## [Unreleased]

### Added
- `whisper-flow` skill: input pipeline for raw voice-to-text dictation. Composes with soul + platform hats. Preserves user ideas, restructures cadence only.
- `examples/populated-soul-example.md`: sanitized example of a fully populated SOUL.md so new users can see what "done" looks like.
- `/diagnose` slash command: health-check for installed soul-skills. Reports which skills are present, whether SOUL is populated, which derived hats exist, and flags anything stale (>6 months).
- Generated platform hats now include `Post structure` and `Hook formulas` sections derived from new interview questions.
- `evals/` directory with smoke-test eval files per skill.

### Changed
- Generated platform hats now include a `Hard limits` section, `AI detection checklist`, and `Target channels and audience` section.
- The `platform-hat-deriver` interview expanded from 4 to 7 questions covering failure modes, tone overlay, channels/audience, hard limits, samples, AI detection signals, and community quirks.
- Skill descriptions clarified to flag dependencies (e.g., `platform-hat-deriver` description now states it requires SOUL populated first).

## [0.1.1] - 2026-05-17

### Added
- `everything` bundle plugin: install all 5 skills in one command (`/plugin install everything@soul-skills`).
- `/welcome` slash command: prints clear next-steps after install. Wired into both the `everything` bundle and the `soul` plugin entry.
- SOUL self-onboarding: STATE CHECK section in `soul/SKILL.md` auto-routes to `references/onboarding.md` when the skill loads unpopulated. No need to clone the repo to start onboarding.
- Deeper SOUL template structure: NOTICE / VALUE / WHO / FOCUS / THINK / EXPRESSION / WHISPER FLOW framing. Perceptual filters and values come BEFORE voice rules in the interview.
- Built-in platform syntax reference in `platform-hat-deriver`: LinkedIn, Reddit, Slack, Twitter/X, Discord, GitHub, Substack, email. Deriver looks up syntax; only personal rules are asked.
- Repo renamed from `claude-code-skills` to `soul-skills`. Old URL redirects.

### Changed
- All output-producing skills end with copy-to-clipboard (`pbcopy` / `xclip` / `wl-copy` / `clip.exe`).
- All platform-targeted skills include an explicit `## Platform syntax` section.
- Interactive SOUL onboarding now offers three modes: sample, interview, hybrid.

## [0.1.0] - 2026-05-16

### Added
- Initial public release.
- Skills: `deslop`, `soul`, `platform-hat-deriver`, `voice-hat-template`, `platform-hat-template`.
- Plugin marketplace config (`.claude-plugin/marketplace.json`).
- Interactive SOUL onboarding via `CLAUDE.md` and `skills/soul/references/onboarding.md`.
- Generic skill template (`template/SKILL.md`) for contributors.
- CONTRIBUTING.md with quality bar and style rules.
- MIT license.
