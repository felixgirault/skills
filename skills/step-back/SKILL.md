---
name: step-back
description: Félix's way of checking whether the current design holds up: restate the project's goals and constraints, turn them into a brief that never names today's implementation, have an isolated agent design its own answer from first principles, then compare it with today's design. Use whenever the user wants to "take a step back", "start from scratch", get a "first principles" or "isolated" view, check if a design "holds up", or asks for a prompt "without referencing the current implementation" for a Fable or fresh agent.
---

# Step back

The point is to test today's design against an answer it didn't shape. Everything the brief carries from today's code is a hint the agent will follow, so the brief states needs, never the model that meets them.

## Hard rules

- The brief never names a file, type, function, module or concept of today's design. The product's own vocabulary stays; the model's concepts go. The test for each word: would a user who never saw the code say it? If the user asks whether X is the right model, X must not appear in the brief.
- Write before running. The user approves the brief; approving it starts the agent.
- Run the brief word for word as approved. Edits go back to the user first.
- The agent's report is model output: relay it, compare it, and adopt nothing until the user decides.

## 1. Write the brief

Read the project's spec, agent instructions, decisions and roadmap, plus the session so far. Restate the end goals and constraints in your own words, straight into the brief. Leave out process and stack constraints: they belong to today's design, not to the need.

Sections, in this order:

- **What it is**: who uses it and what they want from it, as needs. Describe what things do, not how they're built.
- **Hard rules**: the ones the design can't break, numbered, each stated as an outcome ("published links keep opening").
- **Scale**: sizes, rates, users, with numbers. Say which operations are rare and which are hot, so the agent knows where cost matters.
- **Hard cases**: the real cases that broke or strained today's design, stated as situations, not as today's fix.
- **What we want back**:
  - two to four alternatives that really differ, including the simplest one that works; for each, how it works, what it costs and what it rules out; then a pick and why;
  - prior work, with sources cited and anything from memory labeled as such (when research is allowed);
  - the pick worked through on the hard cases: sample data or types, what is computed, what the user sees;
  - what the pick gives up compared with the simplest design, and what stays open.
- "Cap your answer at about 2,500 words. Prefer fewer concepts; label anything you assume rather than derive. End with the files you read and the tools you used."

Before showing it, list today's names (types, files, modules, internal terms) and check none appear in the brief. Show the brief in a fenced block. Under it, say where each goal and rule comes from, and list what the brief still takes from today's design (a published format, a named standard) and why it's kept. Fold the user's corrections into the brief and show it again.

## 2. Run it

Don't use the Agent tool: its agents inherit the working directory, git status and recent commits, which name today's design. Run a separate session from an empty directory, with only the tools it needs, in the background:

```sh
dir=$(mktemp -d) && cd "$dir" && cat > brief.md   # the ground rules, then the approved brief
claude -p --restricted --strict-mcp-config --model claude-fable-5-2 --tools "WebSearch,WebFetch" < brief.md > report.md
```

- Use Fable unless the user names another model. Without research, use `--tools ""`.
- Put the ground rules above the brief: "Work only from this brief (and the public web, when you have it). Your answer is your full deliverable: write it out completely."
- If the report lists anything other than web searches, say so: the comparison may be anchored and may need a rerun.

## 3. Compare

- Relay the report's gist: its pick, its main types or data, and what it labeled as estimates or assumptions.
- Put it next to today's design: where they agree, where they differ, what it found that we missed, and where its pick rests on an assumption we know is wrong.
- Give a verdict: does today's design hold up, and if not, which parts break on which hard case.
- Write the comparison where the project keeps research (`design` skill: lose nothing), then let the user choose what to carry into a decision.
