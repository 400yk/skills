---
name: manager-briefing
description: Use when the user asks for a simpler, plain-terms, or manager-readable summary of progress, status, or a decision — e.g. "explain in simpler terms", "give me a manager summary", "recap", "is this done?"
---

# Manager Briefing

## Overview

Claude reports progress like an engineer writing a work log: long, multi-section, full of jargon and step-by-step narration. A human acting as a manager does not need the log. They have limited time and need three things: the situation, the status, and the decision being asked of them.

**Core principle:** Report like a junior worker briefing a busy manager. Detailed engineering work continues underneath — only the communication changes.

## When to Use

Use when the user asks for a simpler, plain-language, or manager-level summary — phrases like:

- "explain in simpler terms"
- "give me a manager summary" / "executive summary"
- "recap" / "where are we"
- "is this done?"

When invoked, the manager brief **is** the response. Do not bolt it onto a verbose dump.

## The Format

### Word budget

The brief stays **under 150 words**. Hard ceiling. The topic menu and any later drill-in answers do not count against it.

### The four questions

Always answer these four internally. Render a section **only when it has real content** — no filler, no empty headers.

1. **Status** — Done / Partially done / Blocked / In progress. Always shown. One word plus one short clause.
2. **What changed** — what is actually different now, in plain terms. Shown when work was done.
3. **Risk** — what could bite us, or what is uncertain. Shown only if real. Never write "Risk: none".
4. **Decision needed** — the one question for the manager, with your recommendation. Shown only when genuinely blocked on their answer.

### Topic menu

After the brief, add one line listing 2–4 topic **labels** the manager could drill into — names of things to explore, not the details themselves:

> Ask me about: the two transcription paths · the test-rewrite cost

Omit the line entirely if there is nothing deeper worth offering.

When the manager drills into a topic, answer it with real detail — that is what they asked for — still in plain language. The 150-word ceiling is lifted for the drill-in answer.

### One question rule

Never present a multi-option technical fork ("overlay vs. signature change vs. pause first"). Ask **one** plain decision question, state your recommendation, and explain why the answer matters.

## Jargon & Tone Rules

**Translate jargon into plain meaning.** Keep exact file or symbol names only when the manager would act on them. Drop raw command output, stack traces, and search counts unless asked.

| Instead of | Say |
|---|---|
| "`screenpipe_service` reads `primary_language`, `emit_partials` from raw TOML via `build_asr_launch_config`" | "one older transcription path still reads user preferences from the old settings file" |
| "Resolved the UU conflict in `lib.rs` and staged it" | "fixed the merge conflict and saved it" |

**Separate facts from recommendations.** Label them. "Here is what is true" versus "here is what I would do." Never blend the two.

**Tone:** calm, direct, plain.

- No drama — not "the picture changed meaningfully".
- No narration spam — not "Let me re-investigate", "Read 1 file", "Searched 3 patterns".
- No filler praise, no thinking out loud.

## Red Flags — STOP

If you catch yourself thinking:

| Thought | Reality |
|---|---|
| "The manager needs this detail to understand" | They need the situation and the decision. Detail goes in the topic menu. |
| "I should show my work so they trust it" | Trust comes from a clear status and an honest risk, not from a transcript. |
| "One more option will not hurt the question" | A multi-option fork makes the manager do your job. Recommend one. |
| "It is only a little over 150 words" | The ceiling is the discipline. Cut until it fits. |
| "Risk: none — I will show the header anyway" | Empty sections are filler. Drop them. |

## Example

**Before** — engineer's work log (verbose, jargon, narration):

> The other agent's ASR billing work changed the consumption-path landscape. There are now two ASR consumption paths, toggled by `use_custom_audio_capture`. The custom audio pipeline (`audio_capture/`, opt-in) reads user settings from `ConfigState.asr_transcription` directly — already migrated. The screenpipe sidecar (`screenpipe_service/`, default) still reads `provider`, `tier`, `cloud_stt_mode`, `primary_language`, `emit_partials`, `combine_input_output_stream` via `build_asr_launch_config` and `bool_from_config` from raw TOML. Let me re-investigate whether the old screenpipe path is still live...

**After** — manager brief:

> **Status:** Partially done. Settings storage is moved and tested; one old path still lags.
>
> **What changed:** User settings (transcription service, language, audio length) now save to the new config file. Tests pass.
>
> **Risk:** The app has two transcription engines. The new one already uses the new file; the older "screenpipe" engine still reads the old file. If users run screenpipe, their settings come from the wrong place.
>
> **Decision needed:** Are we keeping the screenpipe engine? If yes, I will migrate it (a quick compatibility patch now, full cleanup later). If it is being retired soon, I will skip the migration — it would be wasted work.
>
> Ask me about: the two transcription engines · the quick-patch vs. full-fix tradeoff · the test cost
