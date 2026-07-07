# SPEC — How to Use LLMs Efficiently (deck v2)

The spec for the deck's content, structure, and authoring process. Read this
alongside `README.md` (build/publish mechanics) and `.local/notes.md` (local
working notes) at the start of a session.

## What this deck is

A Slidev deck presenting **Harrison's method for using LLMs efficiently** —
the emphasis is *cost*: there may be more effective ways to use LLMs, but this
method keeps token spend down. It replaces the v1 deck ("Using LLMs
Effectively", aimed at beginner coders), which is archived at
`archive/slides-v1.md`. The v2 audience is more technical; the deck is
presented at work.

## Authoring process

- **Harrison dictates the content, claim by claim, in his order.** Do not
  draft slides, propose structure, or research ahead of what he has stated.
- **Claude finds and verifies primary sources for each claim he cites** —
  fetch the source, confirm it actually says the thing, quote it.
- Citations appear as small numbered markers `[n]` on slides; the full
  numbered links accumulate on the final **References** slide.

## Visual style

- One idea per slide. A tiny bit of text; visuals do the work. When a slide
  feels dense, split it across slides rather than shrinking content.
- Established color language: **blue block = user message, amber = model
  reply, faded = re-sent history**. Reuse it for continuity.
- Depth (derivations, caveats, pricing details) lives in presenter notes
  (HTML comments at the end of a slide), not on the slide.

## Settled decisions — don't relitigate

- **Token scaling is described as quadratic, derived — never "exponential" or
  "geometric".** The mechanism is additive (each exchange adds a constant to
  the next read), so reads grow arithmetically (10, 30, 50, …) and the
  cumulative bill is a Gauss sum (= 10·n² in the 10-token model). Punchline:
  "double the conversation, quadruple the bill."
- Sources verified for the statelessness claim: OpenAI *Conversation state*
  guide ("each text generation request is independent and stateless"; even
  stateful mode bills all previous input tokens) and Anthropic *Context
  windows* doc ("input phase: contains all previous conversation history plus
  the current user message"). Both are on the References slide.

## Current slide map

1. **Title** — "How to Use LLMs Efficiently"
2. **Input → Output → Input → …** — growing-bars visual: one row per API
   request, faded history dragged along, v-click reveal per row
3. **An LLM Is a Stateless API Endpoint** — the core claim `[1][2]` + triangle
   motif (centered rows of 1/3/5/7/9 blocks — the per-request read sizes)
4. **Say Every Message Is 10 Tokens** — the walkthrough table (reads
   10/30/50/…, writes constant, history 20n)
5. **The Bill Is a Gauss Sum** — 10 + 30 + 50 + … = 10·n²; linear content,
   quadratic bill
6. **References** — numbered sources, matching on-slide markers

## State / next steps

- Work happens on branch **`deck-v2`**; merges go dev → main when Harrison
  says so. Pushing `main` publishes to Pages, so only push when the deck
  should be public.
- Launch the dev server with the `launch-deck` skill — it kills stale
  instances first (a stale server on 3030 serves old slides; a browser tab
  with a dead hot-reload socket renders stale content until hard-refreshed).
- Slide content beyond slide 5 is **not yet dictated** — wait for Harrison's
  next piece rather than inventing the roadmap.
