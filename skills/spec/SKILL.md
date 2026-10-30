---
name: spec
description: Keeps the project's spec up to date. Use whenever a change alters what the project does or how it behaves (new feature, fix, removed or changed behavior, new constraint), so the spec stays the source of truth for agents.
---

# Spec

The spec describes what the project does, for agents. It is not user documentation.

## Where

- Use the existing spec if the project has one.
- Otherwise create `doc/spec.md`.
- If it grows past about 200 lines, split it into `doc/spec/<topic>.md` files and keep `doc/spec.md` as a short index linking them.

## What

- Behavior, rules, constraints, edge cases and invariants: what must hold true.
- Not implementation details the code already shows, history or rationale (those belong in ADRs and commits).

## How

- Terse: bullet points and short sentences, no prose and no filler.
- Edit the relevant section in place; the spec states what is true now, never a changelog.
- Remove what is no longer true.
- Update it in the same commit as the change it describes.
