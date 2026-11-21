---
name: design
description: Félix's way of working out a solution before any code: scoping, researching prior work, weighing options, challenging them, reviewing the decision and splitting the work. Use whenever a feature, redesign or problem needs thinking through ("new feature: X", "what would it take to…", "how would you go about…", "challenge the idea", "what's next?"), and from the `feature` skill before its ADR is approved.
---

# Design

Design ends with an approved decision (the ADR, in the `feature` skill) and the work split into steps. Until then, no code.

## Hard rules

- A discussion is not a go. Until the decision is approved, write no code and run no build. Only edit design docs: the ADR, research notes and the roadmap. A question is a question, not a request to change something.
- When the user asks for options or your take, give them and stop; don't pick one and build it. Ask before writing anything long.
- Check every claim against the code, the source, the docs or a measurement. A number from memory is a guess: check it or label it. Say what you did not check, and offer to check it. When told to check, check everything, not a sample.
- Lose nothing. Write findings, the gist of each exchange and deferred ideas to where the project keeps them: research docs, the ADR, the roadmap. When rewriting a doc, confirm every item survived.
- The user's scope is the scope. Don't drop cases they listed or swap their terms for yours. Don't add what they didn't ask for. Their examples illustrate; they are not limits. Name what you leave out and why.

## 1. Scope

- Read the project's principles and rules first (spec, design doc, agent instructions), then the past decisions the area touches. Read the git history when a choice looks odd; it may have a reason.
- A terse opener ("new feature: X", an item's name): find the item in the roadmap, ideas, ADRs and code. Restate it in one or two sentences, including what it is not.
- "What's next?": rank the ready items, from the roadmap and the follow-ups of recent decisions, with a one-line reason each. The user picks.
- An open question ("what would it take", "your take first"): answer it with the cost and what it gains. Start nothing until asked.
- The user's own idea: build on it, don't replace it. Still weigh it against alternatives, and say plainly if it is weak.
- When the user wants first principles ("define guidelines first"), don't anchor on what the code does today.
- Ask only the questions that block the design. Number them, make each stand alone, and give your recommended answer.

## 2. Research

Unless the problem is purely internal, research before proposing:

- Prior work: how established tools, standards and the field solve it, and what they call it. Is it already solved by an algorithm, a library or a standard? Borrow ideas; copy only when asked.
- Primary sources over memory: official docs, the actual source code, specs, papers, manuals. Cite them. List any source you can't reach, so the user can fetch it.
- The project's own data: measure on real cases (fixtures, demos, production-like data) rather than estimate.
- Large surveys: one parallel research agent per tool or question.
- Write it up where the project keeps research, with sources, so it is never redone.
- Go lateral (other fields, analogies, a wild pass) only when asked.

## 3. Options

- Give two to four options that really differ, including the simplest one and the one you would build from scratch. For each, say how it works, what it costs and what it breaks or rules out. Then give your pick and why.
- Show, don't tell: a small before and after (an ASCII sketch, sample input and output, a script) on the hardest real case the project has.
- When paper can't settle it, propose a cheap prototype on a branch, or trying both ideas, each on its own branch.
- Take terse answers as decisions ("2", "go with X, but…"). Fold in the constraint they add. What the user accepts only in part goes to the roadmap.
- When challenged, defend your pick with evidence, or concede and say what was wrong with it.

## 4. Challenge it before the user does

Run these questions on your pick before presenting it, then again on the draft:

- **Principles**: does it keep the project's stated principles and rules? Is there one way to do the thing, no special case, the same rules everywhere? If it must break a rule, say so and propose changing the rule.
- **Necessity**: is every part needed? Is any number arbitrary? Are we overdoing it?
- **From scratch**: would you build it this way with no code yet? Does it fix the root cause, or is it a patch the next fix will revert?
- **Model**: where does it belong (data or view, which part owns it)? Does it keep its meaning when its owner is moved, copied or reused?
- **Robustness**: watch for heuristics, conventions and hardcoded paths that break when something else changes. Prefer what the code enforces over what people must remember.
- **Coverage**: does it fit every case the domain has (other cultures and languages, extreme sizes, odd data) and the futures already planned?
- **Loss**: what could a user do before that they no longer can? Is it better than what it replaces?
- **Reach**: what does it change on every surface: UI, file format, API, CLI or script, docs, tests, performance, other open decisions?
- **Names**: is each new name plain to the project's audience and free of another meaning in the domain? Does it fit the project's vocabulary? What do other tools call it?
- **Compatibility**: add migrations or compatibility code only for data or users that actually exist. Ask once, then remember the answer.

Examples of the user asking these: "does this fit all kinds of music?", "is the octave param needed?", "starting from scratch, would we still have built this as a graph?", "isn't it best to attach it to the clip? moving it would change its meaning", "rest can mean silence in music".

## 5. Review the decision

- Review your own draft: contradictions, unchecked claims, gaps, the questions above. Number the findings, so the user can answer "fix all" or "fix all but 2".
- Repeat until a review finds nothing. On request, review the architecture further out: implications, limits, strong points.
- Record the alternatives rejected and why, and what was deferred and where it went.
- Approval can come without a go ("approve, but don't start"). Commit the decision and stop.

## 6. Split the work

- One decision per cohesive change. A family of similar things can share one decision and be built one at a time.
- Put prerequisites first, and make each step usable and reviewable on its own. Order the steps so none builds what a later one deletes.
- When the work is large or uncertain, build a rough or cheap version first, and let the user's reaction to it decide the next step.
- Deferred parts go, by name, to the roadmap or to the decision's "later" list.
- To design something else while a build runs, work in a worktree from main and bring the branch back when done.

## When corrected

- Fix it. Then ask whether it should become a rule, and where: this skill, the project's agent instructions, or a check that enforces it. Reread the rule and confirm you would follow it.
