# Skills

A collection of reusable skills. Each skill lives in its own folder with a `SKILL.md`
that the agent reads when the skill applies.

## systematic-debugging

**What it is:** A step-by-step method for fixing bugs the right way — find out *why*
something broke before changing anything.

**The one rule:** Don't apply a fix until you understand the root cause. A patch that
hides the symptom isn't a fix.

**How it works — four phases, done in order:**

1. **Investigate** — Read the actual error. Reproduce it reliably. Check what changed
   recently. Add logging to see where things break.
2. **Analyze the pattern** — Find working code that's similar. Compare it to the broken
   code. List every difference.
3. **Form a hypothesis** — Write down one specific theory of the cause. Test it with the
   smallest possible change. If it's wrong, form a new theory — don't pile on more fixes.
4. **Implement** — Write a test that fails because of the bug, apply one fix at the root
   cause, then confirm the test passes and nothing else broke.

**Why bother:** Guessing at fixes feels faster but usually isn't — it creates new bugs
and wastes hours. Working the phases takes 15–30 minutes and gets it right the first
time far more often.

**When to use it:** Any bug, test failure, crash, build break, or "that's weird"
moment — especially when you're under pressure and tempted to just try something.

**Extra techniques in the folder:**

- `root-cause-tracing.md` — trace a bug backward through the call stack to its source
- `defense-in-depth.md` — add validation at every layer so the bug can't come back
- `condition-based-waiting.md` — fix flaky tests by waiting for a real condition instead
  of a guessed delay
- `find-polluter.sh` — script that bisects a test suite to find which test leaves a mess
- `test-academic.md`, `test-pressure-1/2/3.md` — scenarios used to validate the skill

See [`systematic-debugging/SKILL.md`](systematic-debugging/SKILL.md) for the full skill.

## manager-briefing

**What it is:** A reporting style that turns Claude's verbose engineering work-logs
into a short status update a busy manager can act on.

**The one rule:** The brief comes first and stays under 150 words — situation, status,
decision. Detail is offered as a topic menu, not dumped.

**How it works:**

- **The four questions** — every brief answers Status, What changed, Risk, and Decision
  needed. Sections with no real content are dropped, not filled with filler.
- **Topic menu** — 2–4 labels of things the manager *could* drill into. Details appear
  only when asked.
- **One question rule** — never a multi-option technical fork; ask one plain question
  with a recommendation.
- **Jargon & tone** — technical names translated to plain meaning, facts kept separate
  from recommendations, no narration spam.

**When to use it:** On-demand — say "explain in simpler terms", "give me a manager
summary", "recap", or "is this done?"

See [`manager-briefing/SKILL.md`](manager-briefing/SKILL.md) for the full skill.
