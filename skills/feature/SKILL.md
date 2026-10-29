---
name: feature
description: Félix's workflow for building a new feature. Use whenever starting a feature, functionality, enhancement or anything new to build ("add X", "implement Y", "let's build Z"), from first question to a reviewed local branch.
---

# Feature

Code follows the `coding-style` skill.

Two hard stops: no code before the ADR, or skipping it, is approved; never push or open a pull request.

## 1. Understand

- Restate the feature in one or two sentences.
- Read the code it touches before proposing anything.
- Ask only the questions that block the work; pick sensible defaults for the rest and say so.

## 2. Plan

- Branch `feature-<short-slug>` from an up-to-date `main`.
- Write an ADR (`docs/adr/NNNN-slug.md` unless the repo has its own place).
- Keep it short, with no fixed template: cover what matters for this feature (goals, constraints, the chosen approach, the plan).
- When alternative implementations were discussed, record them and why they were rejected.
- For a trivial change, ask whether to skip the ADR; never skip it unasked.
- Once approved, commit it as the branch's first commit.

## 3. Build

- Small steps, each leaving the project working; one commit per step.
- Reuse what the codebase already has before writing anything new.
- If the approach changes, update the ADR in the same commit.

## 4. Check

- Add or update tests where the project has them.
- Run the project's tests, linter and type checker; fix what breaks.
- Reread the whole diff and remove anything the feature doesn't need.
