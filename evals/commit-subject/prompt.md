---
max_turns: 10
allowed_tools: [Read, Glob, Grep, Skill]
---

Write the commit message for this change. Reply with the message only.

The diff makes the settings page show an empty-state line ("No sources yet") when the user has no sources configured. Before, the page showed a blank list. A new unit test covers the empty and non-empty cases.
