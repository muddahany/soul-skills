---
name: read-incoming
description: Use to process incoming text the user received and needs to respond to. Triggers on requests like "what is this person actually asking", "read this thread", "summarize this for me", "what does this client really want", "help me understand this email", "process this RFP", "what's the real ask here", or pastes of long client emails, comment threads, support tickets, DMs, RFP/RFQ messages. Extracts surface ask, real ask underneath, underlying fear or concern, implicit constraints, political context, gaps in their framing, and a recommended response shape. Companion to whisper-flow: whisper-flow listens to YOU, read-incoming listens to OTHERS.
---

# Read-Incoming

## The thesis

People ask for what they think they want, not what they actually need. "Urgent" usually means "broken." "Reliable" usually means "previously burned." "Can we hop on a call?" usually means "I do not trust what you wrote" or "I want to negotiate without a paper trail." Behind every message is a fear, a set of constraints, and a political context.

Reading those layers is the difference between a response that lands and a response that wastes everyone's time.

## When to use

- Long client emails or proposals.
- RFP / RFQ / inbound contract requests.
- Reddit, forum, or social threads where someone asked for advice and the user is considering replying.
- Support tickets, bug reports, customer complaints.
- Slack/Discord/DM messages with mixed signals.
- Comment threads on the user's own posts that need a thoughtful reply.
- Anything multi-paragraph the user needs to process before responding.

## When NOT to use

- Single-line messages with one clear ask ("can you send me X?"). Just answer.
- Casual social chat between friends. Overprocessing reads as cold.
- Messages where the user is venting and does not want a response. Ask first.

## Workflow

### Step 1: Confirm the input

Ask the user to paste the FULL incoming message or thread. If they paste partial, ask for the rest. If multiple messages in a thread, ALL of them. Context is load-bearing.

If the user has SOUL populated, load it. The perceptual filters in SOUL's "What I Notice" section apply during extraction.

### Step 2: Extract the layers

For each layer below, write down what you find. Tag uncertain extractions `[verify]` so the user can spot-check before acting on the brief.

1. **Surface ask:** what the sender literally requested. Quote phrases.
2. **Real ask underneath:** what they probably actually want. Often different from the surface ask.
3. **Underlying fear or concern:** what they are afraid of, frustrated with, or trying to prevent. Common signals:
   - "Urgent" → broken or politically pressured
   - "Reliable" → previously burned
   - "Scalable" → about to break or about to get expensive
   - "Quick question" → not actually quick
   - "Can we hop on a call?" → does not trust written word, or wants to negotiate off-paper
   - "Just wondering" → already decided, looking for validation
   - "Best practice" → wants permission to do the obvious thing
4. **Implicit constraints:** deadline, budget, scope, stakeholders. Things they did not state but you can infer from tone, prior context, or what they omitted.
5. **Political context:** who else is involved, who is the audience for your response (cc, bcc, this will be forwarded), what is the power dynamic.
6. **What they did NOT ask but should have:** gaps in their framing. Often the highest-value insight.

### Step 3: Recommend response shape

- **Length:** short / medium / long.
- **Format:** inline reply / structured doc / call / no response at all.
- **Tone:** aligned with whatever `soul` and platform hat are loaded.
- **Who else to involve.**
- **Open questions to ask back** (versus statements to commit to).
- **Timing:** respond now, sit on it, schedule for tomorrow.

### Step 4: Produce the brief

Use this structure:

```
## Surface ask
[what they literally asked]

## Real ask underneath
[what they actually want]

## Underlying fear
[what they are afraid of, with the signals that point there]

## Implicit constraints
- [constraint 1]
- [constraint 2]

## Political context
[who is watching, who will see this, what dynamic is in play]

## What they did NOT ask
[gaps in their framing worth surfacing]

## Recommended response
- Length: ...
- Format: ...
- Open questions to ask back: [...]
- Things to commit to: [...]
- Things to NOT commit to yet: [...]
- Timing: ...
```

Show the brief to the user. Stop there.

### Step 5: Wait for direction

After the user reads the brief, ask what they want to do:

1. Draft a response now (route to whisper-flow → soul → platform-hat → deslop → clipboard).
2. Save the brief and decide later.
3. Schedule a call instead of writing.
4. Decline or ignore (if the recommendation is "no response at all").

Do not auto-draft. The brief is for the user to react to, not a step to skip past.

### Step 6: If drafting a response, compose with other skills

The pipeline:

```
[incoming text]
       │
       ▼
  read-incoming  ──► BRIEF
                     │ (user reacts, decides what to say)
                     ▼
  whisper-flow   ──► (user speaks raw response if useful)
                     │
                     ▼
  soul           ──► (applies the user's voice)
                     │
                     ▼
  <platform>-hat ──► (applies platform syntax + hard limits + AI detection)
                     │
                     ▼
  deslop         ──► (final universal AI-tell pass)
                     │
                     ▼
              copy to clipboard
```

## Anti-patterns

- Do not pretend to know political context the user did not share. Ask, or tag `[verify]`.
- Do not project fear that is not supported by signals in the text. Quote the signal you read it from.
- Do not skip the "What they did NOT ask" step. Gaps are often the most valuable insight.
- Do not bundle the brief AND a drafted response in one shot. The user must see the brief and react before drafting.
- Do not soften the recommendation. If the right move is "do not respond," say "do not respond."

## Tips

- For very long threads (10+ messages), summarise chronologically first ("Person A asked X, Person B responded Y, then they pivoted to Z"). Without the chronology, political context is unreadable.
- If the same sender has prior messages on the same thread, contradictions between earlier and later messages are signal. Surface them.
- If the user has SOUL populated and SOUL contains a "What I Notice" section, apply those perceptual filters during extraction. The user's lens is what gives the brief its edge over a generic summary.
- The recommended response is a starting point. The user decides. You execute.
