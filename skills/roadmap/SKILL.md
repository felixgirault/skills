---
name: roadmap
description: Keeps the project's roadmap up to date. Use whenever planning work, adding or dropping an idea, or finishing something the roadmap lists ("add X to the roadmap", "what's next?", "we're done with Y"), so the roadmap stays the list of what's planned.
---

# Roadmap

The roadmap lists what the project plans to do. It is not a changelog or a spec.

## Where

- Use the existing roadmap if the project has one (`ROADMAP.md`, `doc/roadmap.md`…).
- Otherwise create `ROADMAP.md`.

## What

```md
## Playback

- Gapless playback
- Crossfade between tracks
  - Needs: Gapless playback

## Sharing

- Export playlists as M3U
  - Unlocks: use in other players
  - Open question: relative or absolute paths?
```

- Theme headings, not priority or time; create a theme only when none fits.
- Each item is a short outcome with a unique name; notes refer to other items by their exact name.
- `Needs:` links to items or conditions it depends on, written once, on the dependent item.
- `Unlocks:` only for value outside the roadmap.
- Optional constraint or open question; details belong in an ADR once work starts.
- Terse: no prose, no dates or estimates unless the user gives them.

## How

- Read the roadmap before suggesting what to work on.
- Ready items have no unmet needs; ask the user about conditions outside the roadmap. Among ready items, suggest first those other items need. The user picks.
- Renaming an item renames it in every `Needs:` that points to it.
- Remove an item when it ships, in the same commit, along with the `Needs:` lines pointing to it.
- Remove an item when it is dropped, and ask the user what to do with the items that need it.
