---
type: llm
weight: 1
---

The reply designs before building:

- Writes no code and proposes no file edits beyond a design doc or ADR; it ends by asking the user to choose or answer, not by starting the build.
- Restates the feature and names what it leaves out.
- Gives two or more options that really differ, each with its cost or what it rules out, and a recommended pick.
- Raises that tags and folders become two ways to organize notes, against the "one way" principle, and proposes how to settle it (tags replacing folders, folders as a kind of tag, or changing the principle).
- Raises where tags are stored, given notes are plain Markdown files (front matter, a sidecar file, an index), and what that does to the files on disk.
- Mentions how other note apps handle tags and folders, or offers to check, without stating unchecked facts about them as certain.
- Asks only questions that block the design, numbered, each with a recommended answer.
