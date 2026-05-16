# Lessons from building 20+ Claude Code skills

Things I wish someone had told me earlier.

## Skill vs subagent: pick by context cost

A skill loads into your current conversation. Its full body stays in context. Good for: checklists, voice rules, workflow templates, anything you reference repeatedly.

A subagent runs in its OWN context window. Returns a summary. Good for: research that generates noise (logs, file scans), tasks with different tool access, work that would bloat your main session with 50+ file reads.

Wrong choice = wasted tokens or polluted context. Skills look cheap but a 2,000-line skill loaded into every turn is not cheap. Subagents look heavy but they keep your main window clean.

## The description field is the most important line

Claude's auto-trigger reads the `description` in frontmatter to decide whether to load the skill. Generic descriptions get ignored. Be aggressively specific about the triggering verbs and contexts.

Bad: `description: Helps with code review`
Good: `description: Use when reviewing a pull request, when the user says "review this PR", or when asked to inspect a code change for issues before merge`

## Keep skills focused

A skill that tries to do five things gets loaded only when Claude is confident about all five. A skill that does one thing well gets loaded reliably.

If a skill grows past ~300 lines, consider splitting it. Long skills bloat every conversation that triggers them.

## Voice skills compound

If you use Claude for ANY public-facing writing (emails, posts, proposals, README files), a personalised voice skill pays for itself within a week. The default LLM register (corporate, hedged, em-dash-heavy) does not sound like any real person.

## Test the negative case

When writing a skill, also write down what the skill should NOT trigger on. Then verify Claude actually skips those cases. Skills that trigger too eagerly get disabled, skills that never trigger get forgotten.

## Layer skills, do not merge them

I have a universal `deslop` skill for general AI-tells AND a personalised `soul` for voice. They compose. One mega-skill would be worse than two focused skills you can invoke together.

## Build for the unpopulated state

If a skill needs user-specific content (like SOUL), assume it ships unpopulated by default and self-detects that state. Put a `STATE CHECK` section at the top of the SKILL.md that routes to onboarding when the skill is fresh. This is what makes plugin-marketplace install actually work for personalized skills.

## Platform syntax is load-bearing

When a skill targets a specific platform (Slack, Reddit, LinkedIn, etc.), encode that platform's syntax explicitly. Markdown variant, bold syntax, header support, mention format, hashtag handling, line breaks, character limits. Generic "format constraints" is not enough. A LinkedIn post written as if LinkedIn renders markdown looks broken when posted.

## Copy-to-clipboard as the last step

If a skill produces text the user will publish, the final workflow step should be `pbcopy` / `xclip` / `clip.exe`. Users should not have to terminal-copy. This sounds obvious. Most public skill repos miss it.

## Genuineness gate over generation

Skills that produce content should refuse to operate on garbage input. SOUL onboarding asks "are these samples GENUINELY YOUR writing?" before extracting. Whisper-flow demands raw dictation, not a polished draft. A few "are you sure?" gates upfront save hours of bad output downstream.
