# Photoshop Drag & Drop Fix · Windows Diagnostic Tool

Adobe Photoshop 2026 (27.x) on Windows can suddenly stop accepting drag-and-drop from File Explorer. This skill runs a 3-step decision tree to find the root cause, **diagnose-only by design** — every step waits for explicit user authorization before doing anything.

## What This Solves

Turns "Photoshop suddenly won't accept file drops" from random guessing into systematic triage:

- **Step 1**: Check `EnableLUA` registry (root cause in ~80% of cases; Microsoft confirms it breaks Windows 11 drag & drop)
- **Step 2**: Check whether Photoshop is running as administrator (another documented root cause from Adobe Community)
- **Step 3**: Reset Photoshop preferences + restart Windows Explorer

If all three pass and the issue persists, escalate to a **File Explorer → Notepad** three-way drag test to isolate whether the problem is at the Windows drag layer or the Photoshop 27.x receiver layer.

## Scope

- ✅ Windows + Photoshop 2026 (27.x) desktop
- ✅ Drag JPG / PNG / TIFF from File Explorer to PS canvas fails
- ❌ macOS (completely different sandbox model)
- ❌ Illustrator / InDesign / Premiere (different process elevation rules)
- ❌ Non-Adobe apps failing Windows drag-and-drop

## Installation

Copy the entire `photoshop-drag-drop-fix/` folder into your skills directory:

- **Claude Code**: `~/.claude/skills/photoshop-drag-drop-fix/`
- **OpenCode / others**: `~/.agents/skills/photoshop-drag-drop-fix/` or `~/.opencode/skills/`

The agent will load this skill automatically on next session.

## Trigger Phrases

Any of the following will activate this skill:
- "Photoshop won't accept drops"
- "PS can't drag files"
- "photoshop drag drop not working"
- "Files dragged to PS don't respond"
- "photoshop can't drag"

## Design Principles

1. **Diagnose ≠ Fix**: Never runs `reg add`, restarts the computer, or deletes files on its own. Each step reports the conclusion independently and shows the fix command; you confirm before anything runs.
2. **Never sets `EnableLUA` to 0**: Common in web tutorials, but Microsoft explicitly forbids this — it reduces system security AND can break Windows 11 drag & drop.
3. **Most common → most obscure**: Three steps ordered by decreasing probability (80% → …). You can exit after any step.
4. **Explicit boundaries**: No macOS fixes, no other Adobe apps, no pressing keys on your behalf.

## File Structure

```
photoshop-drag-drop-fix/
├── SKILL.md            # Agent-facing execution instructions (technical detail)
├── README.zh-CN.md     # 中文文档
├── README.en.md        # This file
└── LICENSE             # MIT License
```

For step-by-step execution details, see [SKILL.md](./SKILL.md).

## Scope of Validity

Tested only against the environment verified at skill creation time. Future Adobe versions (e.g. PS 28.x) may change the drag receiver mechanism, requiring skill updates. If Microsoft alters the `EnableLUA` default in future Windows releases, the Step 1 verdict logic must be revisited.

## Feedback

Found a new root cause or fix? Issues and PRs welcome.

## License

MIT