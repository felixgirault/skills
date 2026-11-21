---
name: feature
description: Félix's workflow for building a new feature. Use whenever starting a feature, functionality, enhancement or anything new to build ("add X", "implement Y", "let's build Z"), from first question to a reviewed local branch.
---

# Feature

Code follows the `coding-style` skill.

Two hard stops: no code before the ADR, or skipping it, is approved; never push or open a pull request.

## 1. Design

- Work the feature out with the `design` skill: scope, research, options, challenges. The ADR below records its decision.

## 2. Plan

- Branch `feature-<short-slug>` from an up-to-date `main`.
- Write an ADR (`docs/adr/NNNN-slug.md` unless the repo has its own place).
- Keep it short, with no fixed template: cover what matters for this feature (goals, constraints, the chosen approach, the plan).
- When alternative implementations were discussed, record them and why they were rejected.
- For a trivial change, ask whether to skip the ADR; never skip it unasked.
- Once approved, commit it as the branch's first commit.

## 3. Build

- Delegate to the `fglt:builder` agent, giving it the ADR path and the branch, and asking for one commit per step, updating the spec in the commit that changes the behavior (`spec` skill), and the last one removing the feature from the roadmap if it is listed there (`roadmap` skill).
- Relay its report: commits, decisions, departures from the ADR, check results.
- Then give a few short, concrete ways for a human to try the feature by hand: the exact command, URL or input, and what they should see. Cover the main path and one edge case.
