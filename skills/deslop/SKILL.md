---
name: deslop
description: Use AGGRESSIVELY before publishing any text drafted or polished with AI help. Catches AI-tells across structural rhythm (sentence-length uniformity, list-of-three patterns), vocabulary (delve, leverage, robust, paradigm, seamless, etc.), copula avoidance, template phrases, and tone red flags. Trigger whenever the user is about to publish, send, post, share, or finalize AI-assisted content of any kind: blog posts, emails, cold outreach, LinkedIn, Reddit, Twitter, Slack, documentation, proposals, cover letters, comments. Also trigger on requests like "check this draft", "does this sound AI", "before I post", "review this", "polish this". Always offer to run this before content leaves the conversation. Platform-agnostic; layer platform-specific deslop on top if available.
---

# Deslop

## Overview

AI-generated text has fingerprints. Most are not em-dashes. The 2026 generation of detectors weights STRUCTURAL RHYTHM as the #1 signal: identical sentence lengths, compulsive lists of three, copula avoidance, and template constructions. Vocabulary is second. Punctuation is third.

**Core principle:** A draft passes deslop when a reader cannot easily say "this was assembled by an LLM" from rhythm, vocabulary, and tone alone, even before reading for content.

This skill is the GATE between AI-assisted writing and slop. If you generated content from scratch with no real input, deslop will not save you. If you spoke or wrote your genuine thoughts and used AI to structure them, deslop catches the residue so what you publish sounds like you.

This is the UNIVERSAL pass for any text draft. Layer platform-specific skills on top for Reddit, LinkedIn, or your own personal voice rules.

Pattern catalog adapted from `conorbronsdon/avoid-ai-writing` with 2026 additions.

## When to Use

- Before publishing any text written or polished by AI
- LinkedIn, blog posts, emails, docs, proposals, social content
- When something "feels like AI" but you cannot name why
- When a piece got flagged as AI-generated and you need to understand why

## Severity Tiers

**P0 — credibility killers, ALWAYS rewrite:**
- Cutoff disclaimers ("As of my last update", "As of my knowledge cutoff")
- Chatbot artifacts ("I hope this helps!", "Great question!", "Feel free to reach out")
- Unsourced authority ("Studies show", "Experts believe", "Research indicates")
- Reasoning scaffolding ("Let me think step by step", "Breaking this down")
- Sycophancy directed at reader ("Excellent point!", "That's a great observation")

**P1 — obvious AI, rewrite:**
- Tier 1 vocabulary (see below)
- Template constructions ("Whether you're X or Y", "It's not X, it's Y")
- Synonym cycling within a paragraph
- Em-dashes (max 1 per 1,000 words)
- Compulsive adjective triads ("robust, seamless, and innovative")
- Heavy bullet structure with bolded leads on every item

**P2 — polish, rewrite if cluster:**
- Tier 3 vocabulary
- Copula avoidance ("serves as", "boasts", "features")
- Uniform sentence/paragraph length
- Generic closers ("only time will tell", "the future looks bright")
- Rhetorical questions as stalling
- Missing bridge sentences between paragraphs

## Vocabulary Tiers

### Tier 1: always replace

delve, leverage, robust, seamless, paradigm, tapestry, beacon, embark, game-changer, utilize, unpack, deep dive, thought leader, synergy, vibrant, intricate, profound, nestled, thriving, bustling, comprehensive, multifaceted, harness (when standalone), navigate (when metaphorical)

### Tier 2: flag in clusters of 2+

foster, elevate, unleash, empower, bolster, resonate, ecosystem (non-technical), cultivate, facilitate, transformative, holistic, paradigm-shifting, mission-critical (non-technical), at the intersection of, spearhead, champion (as verb), curated, hand-picked

### Tier 3: flag at high density (3+ in 500 words)

significant, innovative, effective, dynamic, compelling, unprecedented, sophisticated, valuable, essential, key, crucial, pivotal, vital

## Structural Patterns

### Rhythm (the #1 detection signal in 2026)

Sentence lengths should vary. If three consecutive sentences are within 10% of each other in length, that is a tell. Mix: 4 words, 18 words, 7 words, 22 words. Not: 14, 16, 15, 14.

Paragraph lengths should also vary. Do not write five 3-sentence paragraphs in a row.

### Copula avoidance

AI replaces "is/has" with fancy verbs to feel more authoritative. Catch:
- "X serves as the foundation" → "X is the foundation"
- "Y boasts a vibrant ecosystem" → "Y has a community"
- "Z features sophisticated tooling" → "Z has good tooling"

### Synonym cycling

AI rotates synonyms within a paragraph to avoid repetition. Real writers repeat key terms. If "developers" becomes "engineers" becomes "practitioners" in three sentences, that is a tell.

### Template phrases (cut on sight)

- "Whether you're X or Y..."
- "It's not X. It's Y." (binary contrast pattern, especially in pairs)
- "But what does this mean?"
- "A step forward for [field]"
- "Marked a pivotal moment"
- "At the intersection of"
- "In today's [adjective] world"
- "A new era of"

### Compulsive triads

Three of anything when two would do. Especially adjective triads:
- "robust, seamless, and innovative" → pick one
- "fast, scalable, and reliable" → pick one
- "comprehensive, sophisticated, and powerful" → cut entirely

Triadic parallel SENTENCE structure ("Stuff X. Stuff Y. Stuff Z.") is borderline. Use sparingly and only when it earns its keep through specificity.

### Bold and structure inflation

- More than one bolded phrase per ~500 words
- Headers in posts under 800 words
- Bullet lists with bolded leads on every item
- "Five key takeaways" when content has three
- Numbered lists in casual contexts

## Sentence-Level Tells

- "It's worth noting that..." → cut
- "It's worth mentioning..." → cut
- "Furthermore", "Moreover", "Additionally" → use plain "and" or a new sentence
- "On one hand... on the other hand..." (perfectly balanced) → pick a side or cut one
- "perhaps", "could potentially", "may indicate" (hedging cluster) → state or cut
- "genuine", "truly", "to be honest" (hollow intensifiers) → cut
- "worth reading", "worth your time" (vague endorsement) → say what is worth it
- "I'd recommend..." → "Try..." or "Use..."
- "Here's the thing..." / "The reality is..." → cut, just say the thing

## Tone Red Flags

- **Sycophancy:** "Excellent point!", "Great question!", complimenting the reader
- **Acknowledgment loops:** restating the prompt before answering
- **Vague attributions:** "Studies show", "Experts believe" without names
- **Emotional flatline:** "I was fascinated", "What surprised me" without showing the surprise through specifics
- **Promotional language:** "vibrant hub", "thriving ecosystem", "nestled within"
- **False concessions:** "While X is impressive, Y remains..." without specifics
- **Novelty inflation:** treating routine concepts as discoveries
- **Generic conclusions:** "Only time will tell", "The future looks bright", "It will be interesting to see"

## Workflow

1. **Read the draft fully** before flagging anything.
2. **Severity scan:** group findings by P0 / P1 / P2.
3. **Rhythm check:** measure sentence and paragraph lengths. Flag uniformity.
4. **Vocabulary scan:** check against Tier 1, 2, 3.
5. **Tone scan:** check the red flag list.
6. **Propose specific rewrites** inline, not whole-doc rewrites unless P0 issues are pervasive.
7. **Present revised version + change summary.**
8. **Wait for approval** before treating the rewrite as final.

## Output Format

```
## Severity scan

P0 (always rewrite):
- [line]: [pattern] → [rewrite]

P1 (obvious AI):
- [line]: [pattern] → [rewrite]

P2 (polish):
- [line]: [pattern] → [rewrite]

## Rhythm check

Sentence lengths: [list or summary]
Paragraph lengths: [list]
Verdict: [varied / uniform / borderline]

## Vocabulary hits

Tier 1: [list with quotes]
Tier 2: [list]
Tier 3: [list, only if 3+ in 500 words]

## Deslopped version

[full revised text]

## What changed
- [bullet]
- [bullet]
```

## Context Profiles

Different platforms tolerate different levels of polish. Adjust strictness:

| Context | Tolerance |
|---|---|
| Investor email, cold pitch | Strictest. P0 + P1 + P2 all flagged. |
| Cold outreach | Strictest. Single AI tell tanks reply rate. |
| Reddit, casual social | Strict on structure (P0 + P1), lenient on perfection (humans make typos). |
| LinkedIn | Strict on promotional language and Tier 1 vocab. |
| Blog post, technical writing | Moderate. P0 + P1, P2 only if cluster. |
| Documentation | Lenient. Some polish is fine, but watch sycophancy. |
| Internal Slack | Most lenient. Just kill em-dashes and chatbot artifacts. |

## Anti-Patterns in Deslop Output

- Do not strip ALL polish. Keep precision in technical content.
- Do not add fake roughness ("uhh", "lmao", "smh") to fake humanity. That reads as AI imitating roughness.
- Do not change facts, numbers, or claims.
- Do not add new content to manufacture personality.
- Do not replace one AI pattern with a different AI pattern (swapping "leverage" for "harness" does not help).
- Do not apply platform-specific deslop rules here. Layer a platform skill on top.

## Bottom Line

If a reader can identify your draft as AI-assembled from the first three sentences, none of the content matters. Deslop is the gate, not the polish.
