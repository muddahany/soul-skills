---
name: your-skill-name
description: REPLACE THIS. Anthropic guidance says descriptions are the primary triggering mechanism. State both WHAT the skill does and WHEN it should trigger. Be aggressively specific about trigger phrases, keywords, and use cases. Mention specific contexts. Example pattern: "Use [aggressively/whenever/when] [doing X]. Trigger on [phrase 1], [phrase 2], [phrase 3]. Also load when [context 1] or [context 2]."
---

# Your Skill Name

## Overview

One paragraph: what this skill does and why it exists. Lead with the outcome, not the method.

## When to Use

List concrete triggering contexts. Be specific. These are not just for humans, they help Claude's trigger logic too.

- [Specific user request 1]
- [Specific user request 2]
- [Specific situation 3]

## When NOT to Use

The negative case matters. Listing it prevents over-triggering.

- [Context where this skill should be skipped]
- [Context where another skill is better suited]

## Workflow

Numbered, imperative steps. Tell Claude exactly what to do.

1. [Step one]
2. [Step two]
3. [Step three]

## Output Format

Define what the skill produces. Templates help here.

```
[Example output structure]
```

## Anti-patterns

What the skill should NOT do. Failure modes to guard against.

- [Anti-pattern 1]
- [Anti-pattern 2]

## Tips for Authors

- Keep this file under 500 lines. If it grows past that, split into `references/` subdirectory with pointers.
- Use kebab-case for the skill folder name and the `name:` frontmatter field.
- Use imperative form ("Do X") not third-person ("The skill does X").
- Explain WHY behind rules, not just WHAT. Avoid excessive ALL-CAPS MUST/NEVER patterns.
- The `description` field is the most important line. It is the primary trigger. Iterate on it.
