---
name: clarify
description: Clarify an ambiguous plan, decision, or idea to build shared understanding before acting. Use when requirements are fuzzy, the user wants to align or stress-test thinking, or another skill needs interactive clarification.
---

Build **shared understanding** with the user before acting. Surface hidden assumptions, resolve high-impact ambiguity, and converge on a confirmed model, rather than interrogating every minor detail or drafting the solution early.

## Triage every gap first

Before asking anything, sort each open uncertainty into one of four buckets:

1. **Fact in the environment** (codebase, files, docs, tools): look it up yourself. For non-trivial lookups, dispatch a subagent with a fresh context window so the main context stays focused. Ask independent questions now and hold only questions that depend on the lookup.
2. **Reversible default** (low risk, clear convention, cheap to change later): pick a sensible default and list it under **Assumptions** instead of spending a question on it.
3. **Empirical question** (visual feel, interaction flow, unknown API behavior, performance): flag it as empirical and suggest a quick spike or `/prototype` rather than debating it in chat.
4. **High-impact decision** (hard to reverse, high ambiguity, or wide blast radius): bring it to the user.

## Run small, bias-aware rounds

Work from largest impact inward: goal and non-goals first, then boundaries and core trade-offs, then critical edge cases. Ask **1 to 3 independent questions per round** so the user can reflect deeply and problem and solution can co-evolve. Any question that depends on an unanswered question in the current round waits for the next round.

Match each question's format to its decision type to keep cognitive load low without anchoring the user:

- **Goal, value, or scope call** (only the human can set the priority): ask openly or frame neutral poles, with no recommendation.
- **Structured trade-off** (architecture, interface, behavior under constraints): offer **2 to 3 balanced, contrastive options** (A, B, C), each stating its concrete gain and concrete cost. Share a tentative lean only when backed by a concrete fact, and pair it with the condition that flips the choice (e.g. *"Leaning A because of [fact]; choose B if [condition]"*). Frame choices neutrally rather than making "yes" accept your pick.
- **Fuzzy term or subtle rule**: probe with a **concrete scenario** (*"When X happens while Y is true, should Z happen?"*) to expose tacit assumptions.

Number each question (`Q1`, `Q2`, `Q3`) so the user can reply concisely by number. List any new reversible defaults in a short **Assumptions** note at the bottom of the round so the user can override any one in a word.

## Apply constructive friction

- **Challenge fuzzy or overloaded words** ("fast", "clean", "user", "sync") by asking what they mean concretely here.
- **Surface contradictions** against earlier answers, codebase facts, or stated goals the moment they appear.
- **Probe boundaries** at least once on non-trivial work: ask what is explicitly out of scope and what failure mode is unacceptable.

## Maintain a compact working summary

During multi-round sessions (after major pivots or every 2 to 3 rounds), include a brief **Working Summary** (goal, settled decisions, active assumptions, open points) so earlier precision stays intact and both sides can spot drift immediately. Keep exploration separate from execution: wait for confirmation before drafting code, specs, or final artifacts.

## Close with a comprehension demonstration

Stop questioning once every high-impact decision is settled and all remaining details are safe reversible defaults. Prove shared understanding with a concise **Demonstration**:

1. **Goal and non-goals**: what this achieves and what it explicitly excludes.
2. **Settled decisions**: each key call and the trade-off accepted.
3. **Explicit assumptions**: reversible defaults you will follow unless the user overrides them.
4. **Concrete examples**: 2 to 3 specific scenarios (including at least one edge or failure case) showing how the agreed rules behave.
5. **Empirical or deferred items**: anything to verify via spike or prototype, if applicable.

Wait for the user to confirm or correct this demonstration before acting. Treat any correction as a new input to the loop rather than patching around it silently.
