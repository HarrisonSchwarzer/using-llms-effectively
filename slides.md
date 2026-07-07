---
theme: seriph
title: How to Use LLMs Efficiently
info: |
  A practical guide to using large language models efficiently — keeping
  costs down without giving up results.
  © 2026 Harrison Schwarzer — content licensed CC BY 4.0.
class: text-center
transition: slide-left
mdc: true
---

# How to Use LLMs Efficiently

Commoditized Stochastic Mimesismaxxing

<div class="pt-12 text-sm opacity-70">
Harrison Schwarzer
</div>

<!--
The previous deck lives in archive/slides-v1.md.
-->

---

# Input → Output → Input → …

<div class="mt-14 flex flex-col gap-3 items-start mx-auto w-max">
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 1</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 2</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 3</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 4</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 5</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
</div>

<div v-click class="mt-10 flex gap-8 justify-center text-xs opacity-70">
  <span><span class="inline-block w-3 h-3 rounded bg-blue-500 align-middle"></span> your message</span>
  <span><span class="inline-block w-3 h-3 rounded bg-amber-500 align-middle"></span> model reply</span>
  <span><span class="inline-block w-3 h-3 rounded bg-blue-500 opacity-25 align-middle"></span><span class="inline-block w-3 h-3 rounded bg-amber-500 opacity-25 align-middle ml-0.5"></span> re-sent history</span>
</div>

<!--
Each row is one API request. The faded blocks are the same messages, sent again —
the model reads them all before writing a word. By request 5 you're paying for
nine blocks to say one new thing.
-->

---

# An LLM Is a Stateless API Endpoint

<div class="mt-12 text-2xl leading-relaxed">
No memory. Every request re-sends — and the model re-reads —<br>the <b>entire conversation history</b>. <sup class="text-sm opacity-60">[1][2]</sup>
</div>

<div class="mt-12 flex flex-col gap-1 items-center">
  <div class="flex gap-1 justify-center">
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
  </div>
  <div class="flex gap-1 justify-center">
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
  </div>
  <div class="flex gap-1 justify-center">
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
  </div>
  <div class="flex gap-1 justify-center">
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
  </div>
  <div class="flex gap-1 justify-center">
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-amber-500 opacity-40"></div>
    <div class="w-4 h-4 rounded bg-blue-500 opacity-40"></div>
  </div>
</div>

<!--
Both vendors state this directly: OpenAI's conversation-state guide ("each text
generation request is independent and stateless") and Anthropic's context-windows
doc ("input phase: contains all previous conversation history plus the current
user message"). Even OpenAI's "stateful" mode bills all previous input tokens.
-->

---

# Say Every Message Is 10 Tokens

<div class="mt-10 text-lg">

| Turn | Model reads | Model writes | History after |
|------|-------------|--------------|---------------|
| 1    | **10**      | 10           | 20            |
| 2    | **30**      | 10           | 40            |
| 3    | **50**      | 10           | 60            |
| n    | **20n − 10** | 10          | 20n           |

</div>

<!--
Reads grow arithmetically: each completed exchange adds a constant 20 tokens to
the history, so the next read is 20 bigger. Additive, not multiplicative —
"exponential" would mean each read is a multiple of the last (10, 30, 90, 270…),
which is not what happens.
-->

---

# The Bill Is a Gauss Sum

<div class="mt-16 text-3xl font-mono text-center">
10 + 30 + 50 + … = <b>10·n²</b>
</div>

<div class="mt-16 p-4 bg-amber-500 bg-opacity-10 rounded text-center">
💡 Your content grows <b>linearly</b>. The bill grows <b>quadratically</b>.<br>
<span class="text-lg">Double the conversation, quadruple the bill.</span>
</div>

<!--
Gauss-sum sanity check from prep: 100 messages of 1 token each, if every message
re-read everything so far → 1+2+…+100 = 5050 (T₁₀₀). Actual API billing reads only
on user requests: 100 alternating messages = 50 requests reading 1, 3, 5, …, 99
→ 2,500 input tokens, plus 50 billed as output.

Pricing wrinkle: output tokens cost ~5× input (e.g. Claude Opus 4.8: $5/M input vs
$25/M output), so "total tokens" understates the true cost skew.
-->

---

# The Bill Isn't the Only Thing Growing

<div class="mt-24 text-2xl text-center leading-relaxed">
A growing history doesn't just cost <b>money</b> …
</div>

<div v-click class="mt-6 text-2xl text-center leading-relaxed">
… it costs <b>intelligence</b>.
</div>

<!--
Bridge from cost to quality. So far the problem was the bill; the next slides
show the same growing context also degrades the model's output.

Matt Pocock — TypeScript educator (Total TypeScript), now teaching AI-assisted
coding at AI Hero. This section draws on his "Full Walkthrough: Workflow for
AI Coding" workshop, AI Engineer conference (Europe), April 24, 2026.
-->

---

# The Smart Zone and the Dumb Zone

<div class="mt-14 flex flex-col gap-8 items-start mx-auto w-max">
  <div v-click class="flex items-center gap-3">
    <span class="w-28 text-right text-xs opacity-50 font-mono">200K window</span>
    <div class="flex h-6">
      <div class="rounded-l bg-emerald-500" style="width: 75px"></div>
      <div class="rounded-r bg-rose-500 opacity-30" style="width: 75px"></div>
    </div>
  </div>
  <div v-click class="flex items-center gap-3">
    <span class="w-28 text-right text-xs opacity-50 font-mono">1M window</span>
    <div class="flex h-6">
      <div class="rounded-l bg-emerald-500" style="width: 75px"></div>
      <div class="rounded-r bg-rose-500 opacity-30" style="width: 675px"></div>
    </div>
  </div>
</div>

<div v-click class="mt-8 flex gap-8 justify-center text-xs opacity-70">
  <span><span class="inline-block w-3 h-3 rounded bg-emerald-500 align-middle"></span> smart zone — ends ≈ 100K tokens</span>
  <span><span class="inline-block w-3 h-3 rounded bg-rose-500 opacity-30 align-middle"></span> dumb zone <sup>[3][4]</sup></span>
</div>

<div v-click class="mt-10 text-2xl text-center">
The window grows. The <b>smart zone</b> doesn't.
</div>

<!--
Pocock's terms. Dictionary definition: "Early in a session the agent is in a
'smart zone' — sharp, focused, recall is good. As the session grows it drifts
into a 'dumb zone': sloppier, forgetful, more mistakes." Key line: "Same
model, same harness — just more context."

The ≈100K figure is his marker from the talk: "around 100k is kind of my new
marker for this … it doesn't matter whether you're using 1 million context
window or 200k." His written dictionary says the dumb zone "commonly begins
around 125K–150K tokens — though this is debated." The zones don't track the
window limit — "plan around the smart zone, not the window."

He attributes the felt effect to attention degradation. Echo of our cost
story: attention compute also scales quadratically with context length —
same shape, but presented here as an echo, not as the claimed mechanism.

This is a recreation of the visual from his talk (no published deck exists).
-->

---

# It's Not Just a Feeling

<div class="mt-4 text-center text-xs opacity-60">
NoLiMa benchmark — needle-in-a-haystack with <b>no literal matches</b> <sup>[5]</sup>
</div>

<div class="mt-6 flex justify-center gap-20">
  <div v-click>
    <div class="text-center text-sm mb-1 opacity-80">GPT-4o</div>
    <div class="text-center text-[10px] mb-3 opacity-50">claims 128K · effective 8K</div>
    <div class="flex items-end gap-2" style="height: 119px">
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">99</span><div class="w-7 rounded-t bg-amber-500" style="height: 119px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">98</span><div class="w-7 rounded-t bg-amber-500" style="height: 118px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">96</span><div class="w-7 rounded-t bg-amber-500" style="height: 115px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">89</span><div class="w-7 rounded-t bg-amber-500" style="height: 107px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">82</span><div class="w-7 rounded-t bg-amber-500" style="height: 98px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">70</span><div class="w-7 rounded-t bg-amber-500" style="height: 84px"></div></div>
    </div>
    <div class="flex gap-2 mt-1">
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">base</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">1K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">4K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">8K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">16K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">32K</span>
    </div>
  </div>
  <div v-click>
    <div class="text-center text-sm mb-1 opacity-80">Claude 3.5 Sonnet</div>
    <div class="text-center text-[10px] mb-3 opacity-50">claims 200K · effective 4K</div>
    <div class="flex items-end gap-2" style="height: 119px">
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">88</span><div class="w-7 rounded-t bg-amber-500" style="height: 105px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">85</span><div class="w-7 rounded-t bg-amber-500" style="height: 102px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">78</span><div class="w-7 rounded-t bg-amber-500" style="height: 93px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">62</span><div class="w-7 rounded-t bg-amber-500" style="height: 74px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">46</span><div class="w-7 rounded-t bg-amber-500" style="height: 55px"></div></div>
      <div class="flex flex-col items-center gap-1"><span class="text-[9px] opacity-60">30</span><div class="w-7 rounded-t bg-amber-500" style="height: 36px"></div></div>
    </div>
    <div class="flex gap-2 mt-1">
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">base</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">1K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">4K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">8K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">16K</span>
      <span class="w-7 text-center text-[9px] opacity-50 font-mono">32K</span>
    </div>
  </div>
</div>

<div v-click class="mt-6 text-center text-lg">
Scores collapse long before the window is full.<br>
<span class="text-xs opacity-60">Same pattern across 18 frontier models — even on trivial tasks <sup>[6]</sup></span>
</div>

<!--
NoLiMa (Adobe Research, ICML 2025): 13 LLMs, all claiming ≥128K contexts,
tested on needle-in-a-haystack where question and needle share no words — the
model must infer the association, so the drop is attention, not string
matching. Abstract: "At 32K, for instance, 11 models drop below 50% of their
strong short-length baselines. Even GPT-4o … experiences a reduction from an
almost-perfect baseline of 99.3% to 69.7%." (The repo README says 10 models;
the paper's abstract says 11 — the abstract is canonical here.)

Full table (base / 1K / 2K / 4K / 8K / 16K / 32K → effective length, defined
as the longest length keeping ≥85% of base):
- GPT-4o: 99.3 / 98.1 / 98.0 / 95.7 / 89.2 / 81.6 / 69.7 → 8K
- Gemini 1.5 Pro: 92.6 / 86.4 / 82.7 / 75.4 / 63.9 / 55.5 / 48.2 → 2K
- Claude 3.5 Sonnet: 87.6 / 85.4 / 84.0 / 77.6 / 61.7 / 45.7 / 29.8 → 4K
- Llama 3.3 70B: 97.3 / 94.2 / 87.4 / 81.5 / 72.1 / 59.5 / 42.7 → 2K

Chroma's "Context Rot" report (2025) corroborates on newer models: 18 models
across Claude 4, GPT-4.1, Gemini 2.5, Qwen3 families — "performance grows
increasingly unreliable as input length grows", "even under these minimal
conditions, model performance degrades as input length increases."

Pocock's own context-window article visualizes the related "Lost in the
Middle" effect (Liu et al., TACL 2024) — next slide.
-->

---

# "Lost in the Middle"

<div v-click class="mt-10 mx-auto w-max flex items-center gap-3">
  <span class="text-xs opacity-50" style="writing-mode: vertical-rl; transform: rotate(180deg)">impact on output →</span>
  <div>
    <div class="flex gap-2 items-start pl-5 pb-5" style="border-left: 2px dashed rgba(128,128,128,.4); border-bottom: 2px dashed rgba(128,128,128,.4)">
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 0px; opacity: 1"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 32px; opacity: .8"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 59px; opacity: .63"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 81px; opacity: .49"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 98px; opacity: .39"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 110px; opacity: .31"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 118px; opacity: .26"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 120px; opacity: .25"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 118px; opacity: .26"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 110px; opacity: .31"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 98px; opacity: .39"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 81px; opacity: .49"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 59px; opacity: .63"></div>
      <div class="w-6 h-6 rounded bg-amber-500" style="margin-top: 32px; opacity: .8"></div>
      <div class="w-6 h-6 rounded bg-blue-500" style="margin-top: 0px; opacity: 1"></div>
    </div>
    <div class="text-xs opacity-50 text-center mt-2">position in conversation →</div>
  </div>
</div>

<div v-click class="mt-8 text-center text-2xl">
The start and the end get read. The <b>middle</b> gets skimmed.<br>
<span class="text-xs opacity-60">And it's "much more pronounced the larger the context window gets" <sup>[7][8]</sup></span>
</div>

<!--
Recreation of the diagram in Pocock's "What Is The Context Window?" article
(his version draws the messages as rings on the same U-curve). Opacity here
encodes attention, not re-sent history — every block on this slide *is*
history.

Article, verbatim: "the messages at the start of the history have quite a big
impact on the output, and the ones at the end do too, but the stuff in the
middle the LLM pays a bit less attention to" — "a well-known phenomenon and
it's much more pronounced the larger the context window gets." His diagram's
subtitle notes "this mirrors human behavior" — the serial-position effect
(primacy/recency) from psychology.

The research behind it — Liu et al., "Lost in the Middle: How Language Models
Use Long Contexts" (arXiv Jul 2023, published TACL 2024): "performance is
often highest when relevant information occurs at the beginning or end of the
input context, and significantly degrades when models must access relevant
information in the middle of long contexts, even for explicitly long-context
models."
-->

---

<div class="h-full flex flex-col items-center justify-center">
  <div class="max-w-3xl text-3xl leading-relaxed italic opacity-90 text-center">
    "LLMs are kind of like the guy from <i>Memento</i> — they just continually forget."
  </div>
  <div v-click class="mt-10 text-sm opacity-60">— Matt Pocock <sup>[3]</sup></div>
</div>

<!--
Verbatim from the talk transcript (~7 min mark): "Another weird constraint of
LLMs is LLMs are kind of like the guy from Memento, right? They just
continually forget." Lightly cleaned for the slide.

Memento (2000): Leonard can't form new memories — every scene he starts from
scratch, relying on polaroids and tattoos as external memory. That's the
stateless endpoint from slide 3 wearing a trench coat: nothing persists
between requests; anything the model should "remember" must be written down
and re-sent.
-->

---

# Lost in Conversation

<div v-click class="mt-16 text-center">
  <div class="text-8xl font-bold text-rose-500">−39%</div>
  <div class="mt-4 text-sm opacity-70">average performance when a task arrives in pieces across turns,<br>instead of one fully-specified prompt — 15 top LLMs · six task types <sup>[9]</sup></div>
</div>

<div v-click class="mt-12 text-2xl text-center italic opacity-90">
"When LLMs take a wrong turn in a conversation,<br>they get lost and do not recover."
</div>

<!--
Laban, Hayashi, Zhou, Neville — "LLMs Get Lost in Multi-Turn Conversation"
(Microsoft Research + Salesforce Research, arXiv 2505.06120, May 2025).
15 LLMs from eight model families, 200,000+ simulated conversations, six
generation tasks. Same tasks, two deliveries: one fully-specified prompt vs
the same content "sharded" across turns — the multi-turn delivery loses 39%
on average.

Decomposition (paper body): aptitude drops only 16% ("in a non-significant
way") — but unreliability "skyrockets with an average increase of 112% (more
than doubling)". The model isn't much dumber on average; it's wildly less
consistent.

Mechanism, per the abstract: models "make assumptions in early turns and
prematurely attempt to generate final solutions, on which they overly rely."
The quote on the slide is verbatim (italicized in the abstract itself).

Practical takeaway: don't keep arguing with a lost conversation — restart
fresh with everything you've learned in one fully-specified prompt. Why
doesn't it recover? Next slide: the wrong turn stays in the context.
-->

---

# Context Poisoning

<div class="mt-10 flex flex-col gap-3 items-start mx-auto w-max">
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 1</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-amber-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 2</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-rose-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 3</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-rose-500 opacity-40"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-rose-500"></div>
  </div>
  <div v-click class="flex items-center gap-2">
    <span class="w-24 text-right text-xs opacity-50 font-mono">request 4</span>
    <div class="flex gap-1">
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-amber-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-rose-500 opacity-40"></div>
      <div class="w-9 h-5 rounded bg-blue-500 opacity-25"></div>
      <div class="w-9 h-5 rounded bg-rose-500 opacity-40"></div>
      <div class="w-9 h-5 rounded bg-blue-500"></div>
    </div>
    <span class="opacity-40 text-xs">→</span>
    <div class="w-9 h-5 rounded bg-rose-500"></div>
  </div>
</div>

<div v-click class="mt-6 flex gap-8 justify-center text-xs opacity-70">
  <span><span class="inline-block w-3 h-3 rounded bg-rose-500 align-middle"></span> a wrong reply — and everything built on it</span>
  <span><span class="inline-block w-3 h-3 rounded bg-rose-500 opacity-40 align-middle"></span> the error, re-read on every request</span>
</div>

<div v-click class="mt-8 text-center text-xl">
An error "makes it into the context, where it is repeatedly referenced." <sup class="text-xs opacity-60">[10]</sup><br>
<span class="text-sm opacity-70">GPT-4 can spot <b>87%</b> of its own false claims — when asked separately. <sup>[11]</sup></span>
</div>

<!--
Why a lost conversation stays lost: the wrong turn is re-sent and re-read on
every subsequent request, like all history (slide 2's motif — rose here
extends the dumb-zone color to mean "wrong content"; faded rose is the error
riding along in history).

The term: Drew Breunig, "How Long Contexts Fail" (June 22, 2025), verbatim:
"Context Poisoning is when a hallucination or other error makes it into the
context, where it is repeatedly referenced." His fuller taxonomy — poisoning,
distraction, confusion, clash — is worth a read; poisoning is the one that
fits this deck's arc.

The mechanism: Zhang et al., "How Language Model Hallucinations Can Snowball"
(arXiv 2305.13534, 2023) — "an LM over-commits to early mistakes, leading to
more mistakes that it otherwise would not make." The kicker stat, verbatim:
"ChatGPT and GPT-4 can identify 67% and 87% of their own mistakes" — when the
claim is checked separately, outside the conversation that produced it. The
model knows better; staying consistent with its own context wins anyway.
-->

---

# It's Trained to Agree With You

<div class="mt-12 flex justify-center gap-12">
  <div v-click class="flex flex-col gap-3 w-72">
    <div class="rounded-lg bg-blue-500 bg-opacity-10 border border-blue-500 px-4 py-2 text-sm">I really <b>like</b> this argument. Feedback?</div>
    <div class="rounded-lg bg-amber-500 bg-opacity-10 border border-amber-500 px-4 py-2 text-sm self-end">Compelling — well constructed.</div>
  </div>
  <div v-click class="flex flex-col gap-3 w-72">
    <div class="rounded-lg bg-blue-500 bg-opacity-10 border border-blue-500 px-4 py-2 text-sm">I really <b>dislike</b> this argument. Feedback?</div>
    <div class="rounded-lg bg-amber-500 bg-opacity-10 border border-amber-500 px-4 py-2 text-sm self-end">Unconvincing — it falls apart.</div>
  </div>
</div>

<div v-click class="mt-4 text-center text-sm opacity-60">Same argument.</div>

<div v-click class="mt-10 text-center text-2xl">
<b>Agreement isn't evidence.</b> It's what the training rewards. <sup class="text-xs opacity-60">[12]</sup><br>
<span class="text-xs opacity-60">Humans and preference models prefer "convincingly-written sycophantic responses" over correct ones</span>
</div>

<!--
Sharma et al. (Anthropic), "Towards Understanding Sycophancy in Language
Models" — ICLR 2024. Five state-of-the-art assistants "consistently exhibit
sycophancy across four varied free-form text-generation tasks."

The two panels are an illustrative recreation of the paper's feedback-
sycophancy task (feedback on an argument shifts positive/negative to match
the user's stated like/dislike) — not a real transcript.

The training-reward claim, with the paper's own hedge: sycophancy is "likely
driven in part by human preference judgments favoring sycophantic responses";
"when a response matches a user's views, it is more likely to be preferred";
"both humans and preference models prefer convincingly-written sycophantic
responses over correct ones a non-negligible fraction of the time"; and
optimizing against preference models "sometimes sacrifices truthfulness in
favor of sycophancy."

Tie back to the deck's arc: in a long conversation you've usually stated your
views many times — all of it re-read on every request. Pushing back harder
doesn't produce truth; it produces agreement. (That last step is our framing,
not the paper's — it studied single exchanges.)
-->

---

# References

<div class="text-xs grid grid-cols-2 gap-x-10">
<div>

1. OpenAI — *Conversation state*<br>
   <https://developers.openai.com/api/docs/guides/conversation-state><br>
   "Each text generation request is independent and stateless"; even stateful mode "bills all previous input tokens as input tokens."

2. Anthropic — *Context windows*<br>
   <https://platform.claude.com/docs/en/build-with-claude/context-windows><br>
   "Input phase: contains all previous conversation history plus the current user message."

3. Matt Pocock — *Full Walkthrough: Workflow for AI Coding*, AI Engineer, Apr 24 2026<br>
   <https://www.youtube.com/watch?v=-QFHIoCo-Ko><br>
   "Around 100K is kind of my new marker … it doesn't matter whether you're using a 1 million context window or 200K."

</div>
<div>

4. Matt Pocock — *AI Coding Dictionary: Smart zone*<br>
   <https://www.aihero.dev/ai-coding-dictionary/smart-zone><br>
   "On frontier models, the dumb zone commonly begins around 125K–150K tokens — though this is debated."

5. Modarressi et al. — *NoLiMa: Long-Context Evaluation Beyond Literal Matching*, ICML 2025<br>
   <https://arxiv.org/abs/2502.05167><br>
   "At 32K … 11 models drop below 50% of their strong short-length baselines."

6. Chroma — *Context Rot: How Increasing Input Tokens Impacts LLM Performance*, 2025<br>
   <https://research.trychroma.com/context-rot><br>
   "Performance grows increasingly unreliable as input length grows" — 18 frontier models.

</div>
</div>

---

# References (cont.)

<div class="text-xs grid grid-cols-2 gap-x-10">
<div>

7. Matt Pocock — *What Is The Context Window?*<br>
   <https://www.aihero.dev/what-is-the-context-window><br>
   "The stuff in the middle the LLM pays a bit less attention to … much more pronounced the larger the context window gets."

8. Liu et al. — *Lost in the Middle: How Language Models Use Long Contexts*, TACL 2024<br>
   <https://arxiv.org/abs/2307.03172><br>
   "Performance … significantly degrades when models must access relevant information in the middle of long contexts."

9. Laban et al. — *LLMs Get Lost in Multi-Turn Conversation*, 2025<br>
   <https://arxiv.org/abs/2505.06120><br>
   "An average drop of 39% across six generation tasks … when LLMs take a wrong turn in a conversation, they get lost and do not recover."

</div>
<div>

10. Drew Breunig — *How Long Contexts Fail*, 2025<br>
    <https://www.dbreunig.com/2025/06/22/how-contexts-fail-and-how-to-fix-them.html><br>
    "Context Poisoning is when a hallucination or other error makes it into the context, where it is repeatedly referenced."

11. Zhang et al. — *How Language Model Hallucinations Can Snowball*, 2023<br>
    <https://arxiv.org/abs/2305.13534><br>
    "An LM over-commits to early mistakes, leading to more mistakes that it otherwise would not make."

12. Sharma et al. — *Towards Understanding Sycophancy in Language Models*, ICLR 2024<br>
    <https://arxiv.org/abs/2310.13548><br>
    "Sycophancy is a general behavior of state-of-the-art AI assistants, likely driven in part by human preference judgments favoring sycophantic responses."

</div>
</div>
