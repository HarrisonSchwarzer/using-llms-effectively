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
  reply, faded = re-sent history**. Slide 7 adds: **emerald = smart zone,
  rose = dumb zone**. Reuse both for continuity.
- Side-by-side chart panels must share a **fixed-height bar area** (e.g.
  `style="height: 119px"` on both `flex items-end` rows in slide 8) —
  otherwise each panel grows only to its own tallest bar and the baselines
  don't align.
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
- **Smart zone threshold on-slide is ~100K** (Pocock's marker from the talk);
  presenter notes carry his written dictionary's 125K–150K figure and its
  "though this is debated" caveat. Don't flatten the two into one number.
- **Memento quote**: on-slide wording is lightly cleaned ("LLMs are kind of
  like the guy from *Memento* — they just continually forget."); the verbatim
  transcript wording lives in the presenter note. Cited to the talk video.
- **Cite aihero.dev, never github.com, in slides.md** (see `.local/notes.md`
  for the standing rule). The aihero.dev dictionary URLs 404 to non-browser
  fetchers (bot-blocked) but work in real browsers — verify with a browser
  user-agent, don't conclude they're dead.
- Corroborating data verified: NoLiMa (ICML 2025, arxiv.org/abs/2502.05167 —
  "at 32K, 11 models drop below 50%" of baseline; per-model effective lengths
  2K–8K) and Chroma's *Context Rot* report (18 frontier models). Both on the
  References slide. (NoLiMa's repo README says "10 models"; the paper's
  abstract says 11 — the abstract is canonical.)
- **Slide 7's visual is a recreation, not a copy.** Pocock's smart/dumb-zone
  visual exists only in the talk video — no published image on aihero.dev
  (his context-window article has other diagrams, e.g. "Lost in the Middle"),
  no published slide deck. Recreated in the deck's own color language; keep
  it that way (CC BY deck — no third-party image rights to manage).
- **Slide 9 ("Lost in the Middle") is likewise a recreation** of the published
  diagram in Pocock's *What Is The Context Window?* article (rings on a
  U-curve → our blue/amber blocks). Same rationale: no third-party image in a
  CC BY deck. On this slide opacity encodes *attention*, not re-sent history —
  a deliberate, noted overload of the color language (every block there is
  history). Claim double-sourced: Pocock's article `[7]` + the Liu et al.
  "Lost in the Middle" paper it visualizes (TACL 2024) `[8]`.

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
6. **The Bill Isn't the Only Thing Growing** — transition: growing context
   costs money *and* intelligence
7. **The Smart Zone and the Dumb Zone** `[3][4]` — recreated Pocock visual:
   200K vs 1M context bars, same-size emerald smart zone (≈100K), rose dumb
   zone; "The window grows. The smart zone doesn't."
8. **It's Not Just a Feeling** `[5][6]` — NoLiMa bar charts (GPT-4o,
   Claude 3.5 Sonnet; base→32K), effective lengths; Chroma corroboration line
9. **"Lost in the Middle"** `[7][8]` — recreated diagram from Pocock's
   context-window article: blue/amber blocks on a U-curve (impact on output
   vs position in conversation), opacity tracking attention — full at the
   ends, faded in the middle
10. **Memento quote** `[3]` — big centered quote, no heading
11. **References** — numbered sources, matching on-slide markers; two-column
    grid at text-xs, **max 6 entries per slide** (3 per column — entry 6
    overflowed the single-column layout). More sources are expected as the
    deck grows: continue numbering onto additional "References (cont.)"
    slides rather than shrinking or cramming.
12. **References (cont.)** — entries 7–8

## State / next steps

- Work happens on branch **`deck-shape`** (branched off `deck-v2` after it was
  merged into `dev`); merges go dev → main when Harrison says so. Pushing
  `main` publishes to Pages, so only push when the deck should be public.
- This phase's scope: an agenda slide, aligning the overall presentation
  shape, and a section on Matt Pocock's work (sources are listed in
  README.md's References). The Pocock transition (slides 6–9) is dictated and
  done; the agenda and overall shape still await Harrison's dictation — do
  not draft ahead.
- Launch the dev server with the `launch-deck` skill — it kills stale
  instances first (a stale server on 3030 serves old slides; a browser tab
  with a dead hot-reload socket renders stale content until hard-refreshed).
- Slides 1–12 are dictated and committed. Nothing beyond them is dictated —
  wait for Harrison's next piece rather than inventing the roadmap.
