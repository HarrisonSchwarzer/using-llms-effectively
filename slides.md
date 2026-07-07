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

New deck in progress

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

# References

<div class="text-sm">

1. OpenAI — *Conversation state*<br>
   <https://developers.openai.com/api/docs/guides/conversation-state><br>
   "Each text generation request is independent and stateless"; even stateful mode "bills all previous input tokens as input tokens."

2. Anthropic — *Context windows*<br>
   <https://platform.claude.com/docs/en/build-with-claude/context-windows><br>
   "Input phase: contains all previous conversation history plus the current user message."

</div>
