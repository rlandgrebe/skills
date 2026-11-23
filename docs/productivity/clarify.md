## What it does

`clarify` builds **shared understanding** between you and the agent on an ambiguous plan, decision, or idea before anyone acts on it. Rather than interrogating every minor detail in giant batches or nudging you to nod along with pre-baked answers, it triages uncertainties by risk, asks 1 to 3 focused questions per round, and closes by demonstrating its understanding through concrete examples.

It is **stateless**. It writes no files and works equally well for code, architecture, product direction, writing, or general decisions.

## When to reach for it

Type `/clarify`, or the agent reaches for it automatically when a task is ambiguous or another skill invokes it. Start it as soon as you have a fuzzy idea worth taking seriously, before drafting a spec or writing code.

| What you have | Reach for |
| --- | --- |
| A fuzzy idea, decision, or plan (with or without a repo) | `clarify` |
| A repo where you also want `GLOSSARY.md` and ADRs updated inline | [grill-with-docs](../engineering/grill-with-docs.md) |
| An effort too large to settle in one session | [wayfinder](../engineering/wayfinder.md) |
| A question talking cannot settle (UI feel, interaction flow, API behavior) | [prototype](../engineering/prototype.md) |
| A skill of your own that needs interactive alignment | Invoke `clarify` via the Skill tool |

## Balancing anchoring against cognitive load

Asking nothing produces silent assumptions; asking everything with pre-filled "yes" recommendations produces anchoring and passive rubber-stamping. `clarify` resolves that tension by matching its response to the type of uncertainty:

| Uncertainty type | How the agent handles it |
| --- | --- |
| Fact in the environment (code, files, docs, tools) | Looks it up itself, using a subagent with a fresh context window for heavy exploration |
| Reversible default (low risk, clear convention) | Picks a sensible default and lists it under **Assumptions** instead of burning a question on it |
| Empirical question (visual feel, runtime behavior) | Flags it as empirical and recommends a spike or [prototype](../engineering/prototype.md) instead of debating in chat |
| Structured trade-off (architecture, interface, edge cases) | Presents 2 to 3 balanced, contrastive options with concrete gains and costs; states a lean only when backed by facts, paired with the flip condition |
| Goal, value, or scope decision | Asks openly or frames neutral poles, with no recommendation |

Keeping rounds to **1 to 3 independent questions** prevents fatigue and lets the problem and solution co-evolve as each answer reframes what matters next.

## Closing with a demonstration

Asking "do we have a shared understanding?" proves nothing because both sides can read different meanings into the same abstract summary. On longer runs `clarify` maintains a compact **Working Summary** to prevent multi-turn drift, and it finishes with a five-part **Demonstration**: goal and non-goals, settled decisions, explicit assumptions, 2 to 3 concrete scenarios (including at least one edge or failure case), and any empirical items left to verify. The agent acts only after you confirm or correct that demonstration.

## Common questions

**Where did `grill-me` and `grilling` go?**
They were consolidated into `clarify`. Having both a user-invoked wrapper (`grill-me`) and a model-invoked primitive (`grilling`) added duplicate entry points and brittle wrapper delegation. Because a model-invoked skill is directly reachable by both humans (`/clarify`) and other skills, one skill does both jobs.

**Why 1 to 3 questions per round instead of all independent questions at once?**
Large question batches overload working memory, trigger passive agreement, and lock in early framing before your answers can reshape the problem. Small rounds keep each answer thoughtful and let later questions react to what just surfaced.

**Why doesn't it always attach a recommended answer?**
Pre-filled recommendations framed so "yes" accepts them create strong anchoring and acquiescence bias, especially on product and scope calls where the agent has no special authority. `clarify` reserves defaults for low-risk reversible choices (surfaced transparently under **Assumptions**), uses balanced contrastive options for technical trade-offs, and leaves goal and value decisions unanchored.

**What if a question cannot be answered by talking?**
Say so, or expect the agent to call it out itself. Visual feel, UX flow, and uncertain runtime behavior are empirical questions; the right move is a throwaway [prototype](../engineering/prototype.md) or spike, then bringing what you learned back.

**Do I start a fresh session before writing the spec?**
No. Hand the same conversation straight to [to-spec](../engineering/to-spec.md) so the settled decisions, explicit assumptions, and concrete examples carry directly into the spec.

## It's working if

- Each round arrives with 1 to 3 sharp, independent questions rather than a wall of ten or more.
- Low-risk defaults show up in a short **Assumptions** note you can override in a word, instead of cluttering the questions.
- Trade-off questions lay out real gains and costs for each option rather than nudging you to reply "yes".
- Facts the codebase can answer get looked up rather than asked of you.
- Vague words and contradictions get challenged with concrete scenarios.
- The session ends with a concise **Demonstration** containing concrete edge-case examples, and waits for your confirmation before doing anything.

## Where it fits

`clarify` is both a **standalone entry point** for sharpening any fuzzy idea and the **shared clarification primitive** invoked underneath other skills. [grill-with-docs](../engineering/grill-with-docs.md) pairs it with [domain-modeling](../engineering/domain-modeling.md) at the start of the main build chain (ahead of [to-spec](../engineering/to-spec.md)), while [wayfinder](../engineering/wayfinder.md), [triage](../engineering/triage.md), and [improve-codebase-architecture](../engineering/improve-codebase-architecture.md) call it whenever interactive alignment is needed. When you are unsure which skill or flow fits, [ask-matt](../engineering/ask-matt.md) routes you.
