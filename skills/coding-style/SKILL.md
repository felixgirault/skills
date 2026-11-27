---
name: coding-style
description: Félix's personal coding style. Use whenever writing, refactoring or reviewing code in any language, so new code reads like his own. Covers delegation, building, checking and reporting, code shape, naming, structure, dependencies, debt and commits; formatting is left to each project's formatter.
---

# Coding style

Formatting is the project formatter's job; never hand-tune layout.

## Delegation

- Every code change goes on its branch (`feature-*` or `fix-*`, created from an up-to-date `main` if you are on it). A change to behavior updates the spec in the same commit (`spec` skill).
- Unless you are the builder, hand a change that takes several steps or implements an ADR to the `builder` subagent, with a brief (what to change and why, the files involved) and its branch; then relay its report. The brief carries the decisions; the builder only implements them, never delegating.
- Make a small, contained change yourself, following Build, Check and Report below.
- Never push or open a pull request unless asked.

## Build

- Small steps, each leaving the project working.
- Commit each step unless told not to.
- Reuse what the codebase already has before writing anything new.
- Navigate code with a language-server tool when the harness offers one, loading it first if it is deferred (e.g. `LSP` in Claude Code): definitions, references and callers. Use grep only for plain text (strings, comments, docs and config), or when no language server covers the language.
- If the approach changes from an ADR, update the ADR in the same commit.

## Check

- Add or update tests where the project has them.
- Run tests the way the project's instructions say (AGENTS.md, CLAUDE.md, CONTRIBUTING, the README): which command, which profile, and when.
- Without such instructions:
  - While working, the type checker or compiler only.
  - Once a step is done, only the tests for what it changed, by filter or by file.
  - The full suite and the type checker once, before reporting.
- Finding what a change broke is a filtered run too: the tests of the modules it touches, then the ones that failed, never everything again.
- One build or test command at a time. Two at once fight over the build lock and the CPU.
- Run the linter and fix what breaks.
- Reread the whole diff and remove anything the change doesn't need.

## Report

End with:

- Each commit: its hash and subject, what it changes and why, in a line or two.
- Each decision the brief or request didn't settle (a library, a structure, a trade-off): what you chose and why.
- Each departure from the brief or request: what it said, what you did instead, and why.
- Each debt entry you added (Debt below).
- What the checks returned: which test commands you ran and when, and anything left undone.

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

## Debt

- Log in the project's debt doc (`docs/debt.md` unless the repo has one) what you hit on your path and leave unfixed, when the next person would trip on it too: it cost you time, or it can hide a bug. Not an audit: skip what you only noticed in passing.
  - Surprises: an API, tool or doc that behaves unlike what it says, a README command that fails.
  - Flakiness: a test, build or command that passed only on retry.
  - Limits, always: a workaround or shortcut you took, a case left unhandled, a test skipped or that you couldn't write.
  - Friction that cost you time: a slow build or test, a missing tool, a test or lint already failing before you started.
- Not debt: what you fixed on the branch (the commit says it), planned work (`roadmap` skill), a deliberate trade-off (the ADR), style you would have written differently.
- One terse entry per cause, not per symptom: what, where (file, command), how it showed, and the fix if you know it. Update an existing entry rather than adding a twin.
- Commit an entry with the step that hit it, or on its own when no step did (found while reading or running the checks).
- Remove an entry in the commit that fixes it.

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
