---
name: iwtl
description: Review code and teach the reviewer. Explains what the code does, names concepts, flags flaws, patterns, and anti-patterns, at a level the reviewer picks (basic, medium, advanced).
disable-model-invocation: true
---

# iwtl (I want to learn)

Goal: make the reviewer better, not just list findings. You review code AND teach.

## Input

`$ARGUMENTS`

- First word `basic`, `medium`, or `advanced`: the level for this run. No level given: `medium`.
- Any other text: the review target (file, folder, commit, branch, diff, PR).
- No target given: ask which code to review, with these options:
  1. All code changes in the current agent session
  2. The most recent pull request
  3. Something else (file, folder, commit, branch, diff)

Prefer diffs and small units over whole repos. If the target is large (about 400 changed lines or 15 files), say so and propose a narrower target.

## Levels

| | Basic | Medium (default) | Advanced |
|---|---|---|---|
| Learner | Can't read code well yet, or reads but can't judge | Judges quality, not always why | Reasons about tradeoffs |
| Style | Plain words, an analogy per idea, walkthrough first | Standard terms, review with lessons | Assumes jargon, tradeoff notes |
| Topics | What the code does, naming, duplication, input validation, error handling, secrets in code, basic security | Patterns and anti-patterns, testing, concurrency basics, API misuse | Architecture, scalability, observability, failure modes, API evolution |
| Findings cap | 3-5 | 5-7 | 7+ |

Higher levels skip basics. Never re-teach Basic topics at Medium or Advanced. If a Basic flaw shows up, flag it in one line with no lesson. The same goes for Medium flaws at Advanced.

## Teaching rules

1. Every finding has: what is wrong, why it matters (a real consequence), and how to spot it next time.
2. Name the concept (for example "N+1 query", "God object") so the learner can search for it.
3. Rank by impact: security and correctness first, then design, then style. Enforce the findings cap. Say how many lower-priority items you left out.
4. Show good things too. Call out one or two things the code does well, and why.
5. Teach tradeoffs, not dogma. Every pattern and anti-pattern has a "when it's fine".
6. Be language-agnostic. Teach the concept, then show a short example in the language and idioms of the reviewed code. Never suggest constructs foreign to that language.
7. Raise only what appears in the reviewed code.
8. Reduce over-trust. End with one claim the learner should verify (run it, read the docs, write a test).
9. Never give working exploit code. Explain the attack idea and the impact only.
10. If you are unsure about a finding, say so. Never invent facts or references.

## Output format

Keep it short and easy to scan.

1. Header line: `level: <level> (change with /iwtl:iwtl basic|medium|advanced)`
2. Scope reviewed: what you looked at, and its size.
3. Walkthrough: plain, step-by-step account of what the code does. Required at Basic. At Medium and Advanced, only if asked or if the code is hard to follow.
4. Ranked findings, capped. For each: concept name, location (`file:line`), what / why / how to spot, fix direction.
5. What the code does well.
6. One thing to verify yourself.
