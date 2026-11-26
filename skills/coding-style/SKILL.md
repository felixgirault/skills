---
name: coding-style
description: Félix's personal coding style. Use whenever writing, refactoring or reviewing code in any language, so new code reads like his own. Covers code shape, naming, structure, dependencies and commits; formatting is left to each project's formatter.
---

# Coding style

Formatting is the project formatter's job; never hand-tune layout.

## Delegation

- Unless you are the `fglt:builder` agent, never write code yourself: hand every code change to the `fglt:builder` agent with a brief (what to change and why, the files involved) and its branch (`feature-*` or `fix-*`, created from an up-to-date `main` if you are on it), asking it to update the spec in the commit that changes the behavior (`spec` skill), then relay its report.
- The brief carries the decisions; the builder only implements them.

## Precedence

1. The language's idiom and the framework's conventions win (e.g. Adonis classes with DI and decorators, Svelte 5 runes, Astro slots).
2. Existing repo patterns win next (e.g. a repo already on Redux and lodash keeps them).
3. Everywhere else, apply the rules below.

## Code shape

- Illegal states unrepresentable: whatever the compiler can catch, it catches, and tests come after, for what types can't say (behavior over time, output, prose). A rule is held by the code, not by a check someone must remember: a type, one enum (a string-literal union in TS) in place of flags that must agree, an exhaustive match with no wildcard, a field with no default, or a private field behind its one writer.
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

- Subject: what changed, and why if it fits. A short English phrase, at most 72 characters, capitalised, no prefix, no period.
- Pick the tense by who does the verb:
  - The developer, to the code (add, fix, remove, rename, make, delegate…): past tense. "Fixed APCA contrast of simulated colors", "Added album highlights", "Made the builder navigate code with LSP".
  - The software, at runtime (announce, ignore, show, offer…): `-ing` form, since it keeps doing it after the commit. "Announcing saved settings, unsaved entries and recordings", "Ignoring URL changes of background tabs", "Offering to record time on issue pages".
- Check a past-tense subject by reading "This commit <subject>": "This commit showed the empty line only for an empty chart" or "kept commit subjects short" isn't true of the commit, so use the `-ing` form or a verb for what the developer did ("Capped…").
- Body only when the subject isn't enough: what the diff doesn't show (behavior, edge cases, ADR or issue, what the tests cover), wrapped at 72, after a blank line (a second `-m` or a heredoc), never on the subject line.
  ```
  Made lanes meet only through buses

  A wire between two lanes that isn't to or from a bus is refused while
  dragged and on release. One already in a file is drawn in the warning
  color.

  ADR 0242. Tested on the wires a lane may make.
  ```
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
