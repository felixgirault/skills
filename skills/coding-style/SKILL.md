---
name: coding-style
description: Félix's personal coding style. Use whenever writing, refactoring or reviewing code in any language, so new code reads like his own. Covers code shape, naming, structure, dependencies and commits; formatting is left to each project's formatter.
---

# Coding style

Formatting is the project formatter's job; never hand-tune layout.

## Precedence

1. The language's idiom and the framework's conventions win (e.g. Adonis classes with DI and decorators, Svelte 5 runes, Astro slots).
2. Existing repo patterns win next (e.g. `db` keeps React, Redux, sagas, lodash).
3. Everywhere else, apply the rules below.

## Code shape

- Tiny single-purpose functions that compose. If the body is a single expression, return it directly.
- Braces on every `if`, even one-liners, where the language has braces.
- A blank line between logical steps inside a function, and before the final `return`.
- Classes only for real encapsulated state (stores, indexes); plain data and functions otherwise.

## Naming

- Long and explicit: `angleFromAdjacentAndHypotenuse`, `isLuminosityAnalysisEnabled`.
- Conversions: `xToY` or `yFromX` (`rgbToSchemist`, `hslFromCulori`), in the language's casing.
- Name results like the value they return: `shuffled(array)`, `unique(items)`, `withoutIndex(items, i)`.

## Structure

- Many small files grouped by domain (`color/conversion`, `color/contrast`), no `utils` dumping ground. Split rather than grow.

## Dependencies

- Standard library first. Add a small, focused package only for a specific job (color science, feed or cron parsing, geometry); no catch-all utility libraries.

## Comments

- `@see <url>` above borrowed algorithms; the formula above dense maths. Little else.

## Commits

- Short English phrase in the past tense, capitalised, no prefix, no period: "Fixed APCA contrast of simulated colors", "Added album highlights".
- `feature-*` / `fix-*` branches merged through PRs.

## TypeScript / JavaScript

- `export const name = (args) => ...`, never `function` declarations (except `function*`):
  ```ts
  export const hslToSchemist = (color: HslColor): SchemistColor =>
  	rgbToSchemist(rgbFromCulori(convertHslToRgb(hslToCulori(color))));
  ```
- `#private` fields, not `private`.
- String-literal unions, not enums: `type SourceType = 'curated' | 'feed' | 'mailbox'`.
- Named exports for logic; default exports only for components and framework classes.
- No lodash, UI kits or state libraries in new code.
